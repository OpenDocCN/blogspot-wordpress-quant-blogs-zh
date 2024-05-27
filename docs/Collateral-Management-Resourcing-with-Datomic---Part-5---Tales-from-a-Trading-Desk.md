<!--yml

分类：未分类

日期：2024 年 5 月 18 日 05:48:40

-->

# 使用 Datomic 进行抵押品管理资源配置 - 第五部分 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2014/06/18/collateral-management-resourcing-with-datomic-part-5/#0001-01-01`](https://mdavey.wordpress.com/2014/06/18/collateral-management-resourcing-with-datomic-part-5/#0001-01-01)

在与 Spring Data 的有趣经历后 😦 ，我决定快速查看[Datomic](http://www.datomic.com/)，尽管最初计划是从存储库的角度使用 Neo4j。Datomic 本质上具有我之前博客中介绍过的双时视图。就目前的练习而言，我选择了免费的[下载](http://www.datomic.com/get-datomic.html)，因为这基本上是一个概念验证（PoC）。

初始模式：

```

[
;; Team schema

{:db/id #db/id[:db.part/db]
:db/ident :project/name
:db/valueType :db.type/string
:db/cardinality :db.cardinality/one
:db/fulltext true
:db/doc "A project name"
:db.install/_attribute :db.part/db}

{:db/id #db/id[:db.part/db]
:db/ident :team/name
:db/valueType :db.type/string
:db/cardinality :db.cardinality/one
:db/fulltext true
:db/doc "A team name"
:db.install/_attribute :db.part/db}

{:db/id #db/id[:db.part/db]
:db/ident :person/name
:db/valueType :db.type/string
:db/cardinality :db.cardinality/one
:db/fulltext true
:db/doc "A person name"
:db.install/_attribute :db.part/db}

{:db/id #db/id[:db.part/db]
:db/ident :team/people
:db/valueType :db.type/ref
:db/cardinality :db.cardinality/many
:db/fulltext true
:db/doc "A teams ref to people"
:db.install/_attribute :db.part/db}
]

```

一些测试数据

```

[
{:db/id #db/id[:db.part/user -1], :person/name "Bob"}
{:db/id #db/id[:db.part/user -2], :person/name "Fred"}
{:db/id #db/id[:db.part/user -3], :person/name "John"}
{:db/id #db/id[:db.part/user -4], :project/name "Risk Project 1", :team/name "Risk Feature Team 1", :team/people #db/id[:db.part/user -1 :db.part/user -2]}
{:db/id #db/id[:db.part/user -5], :project/name "Risk Project 2", :team/name "Risk Feature Team 11", :team/people #db/id[:db.part/user -3]}
{:db/id #db/id[:db.part/user -6], :project/name "Risk Project 3", :team/name "Risk Feature Team 111"}
]

```

样本代码，部分借用自 Datomic 示例：

```

package datonicplay;

import datomic.*;

import java.io.FileReader;
import java.io.Reader;
import java.util.Collection;
import java.util.List;
import java.util.Scanner;

public class dplay {
    public static void main(String[] args) {
        final dplay teamPlay = new dplay();
        teamPlay.run();
    }

    private void run() {
        try {
            System.out.println("Creating and connecting to database...");

            final String uri = "datomic:mem://teams";
            Peer.createDatabase(uri);
            final Connection conn = Peer.connect(uri);

            System.out.println("Parsing schema edn file and running transaction...");

            final Reader schema_rdr = new FileReader("src/main/java/data/teams-schema.edn");
            final List schema_tx = (List) Util.readAll(schema_rdr).get(0);
            Object txResult = conn.transact(schema_tx).get();
            System.out.println(txResult);

            System.out.println("Parsing seed data edn file and running transaction...");

            final Reader data_rdr = new FileReader("src/main/java/data/team-testdata.edn");
            final List data_tx = (List) Util.readAll(data_rdr).get(0);
            data_rdr.close();
            txResult = conn.transact(data_tx).get();

            System.out.println("Finding all teams, counting results...");

            Collection results = Peer.q("[:find ?match :where [?match :person/name]]", conn.db());
            System.out.println(String.format("Number of people: %d", results.size()));

            final Database db = conn.db();
            for (Object result : results) {
                final Entity entity = db.entity(((List) result).get(0));
                System.out.println(String.format("%s %s", entity.toString(), entity.get(":person/name")));
            }

            results = Peer.q("[:find ?match :where [?match :project/name \"Risk Project 1\"]]", conn.db());
            System.out.println();
            System.out.println(String.format("Number of teams in \"Risk Project 1\":%d", results.size()));

            for (Object result : results) {
                final Entity entity = db.entity(((List) result).get(0));
                System.out.println(String.format("%s %s %s", entity.toString(), entity.get(":team/name"), entity.get("team/people")));
            }

            results = Peer.q("[:find ?read :where [?read team/people] [?match :project/name \"Risk Project 1\"]]", conn.db());
            System.out.println();
            System.out.println(String.format("Number of people in \"Risk Project 1\" teams:%d",results.size()));

            for (Object result : results) {
                final Entity entity = db.entity(((List) result).get(0));
                System.out.println(String.format("%s %s", entity.toString(), entity.get(":team/people")));
            }

            results = Peer.q("[:find ?read :where [?read :team/name \"Risk Feature Team 1\"]]", conn.db());
            System.out.println();
            final Entity team = db.entity(((List) results.iterator().next()).get(0));

            results = Peer.q("[:find ?c_name ?r_name :where " +
                            "[?c :team/name ?c_name]" +
                            "[?c :project/name \"Risk Project 1\"]" +
                            "[?r :team/people ?r_name]]",
                    conn.db());
            for (Object result : results) System.out.println(result);

            Peer.shutdown(true);

        }
        catch (Exception e) {
            e.printStackTrace();
            System.exit(-1);
        }

    }

    private static final Scanner scanner = new Scanner(System.in);

    private static void pause() {
        if (System.getProperty("NOPAUSE") == null) {
            System.out.println("\nPress enter to continue...");
            scanner.nextLine();
        }
    }
}

```

显然是一个正在进行中的工作。最后两个查询完全不正确。我似乎没有提供一个合理的查询来提供“风险特性团队 1”团队中的所有人员的列表

~ 由 mdavey 于 2014 年 6 月 18 日发布。

发布在 [Data](https://mdavey.wordpress.com/category/data/)，[Languages](https://mdavey.wordpress.com/category/languages/) 中
