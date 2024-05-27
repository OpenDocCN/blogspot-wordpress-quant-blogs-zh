<!--yml

类别：未分类

日期：2024-05-18 05:26:44

-->

# 通过 DiffBlue 避免构建破坏者 | 从交易台的故事中汲取经验

> 来源：[`mdavey.wordpress.com/2019/02/13/avoiding-the-build-breakers-with-diffblue/#0001-01-01`](https://mdavey.wordpress.com/2019/02/13/avoiding-the-build-breakers-with-diffblue/#0001-01-01)

## 通过 DiffBlue 避免构建破坏者

ABN Amro 通过这篇[文章](https://medium.com/abn-amro-developer/improved-software-delivery-within-abn-amro-by-continuous-integration-continuous-delivery-1e317f7fb8cc)提供了关于其持续集成持续交付（CICD）、工具、软件质量和安全性的见解。有趣的是，他们通过“构建破坏者”部分地提高了质量。这些破坏者的问题在于，对于那些明确了标准的新项目来说，这是可以接受的，但是老项目在能够遵循这些标准之前需要跨越一定的障碍。

解决方案？[DiffBlue](https://www.diffblue.com/)

如何做到的？如果您将 DiffBlue 添加到 CI/CD 流水线中，那么如果您的项目代码覆盖率下降到低于％的破坏者，DiffBlue 可以创建单元测试，快速使您的覆盖率超过破坏者。

将老旧项目/产品转移到你漂亮闪亮的 CI/CD 流水线中，也可以借助 DiffBlue。在迁移到 CI/CD 流水线之前生成一个“[完整的回归套件](https://www.diffblue.com/datasheet)”可能会有所帮助。问题解决了。现在迁移已经成为构建破坏者质量解决方案的一部分，而不需要雇佣人员 🙂

最后，[加速](https://www.amazon.co.uk/dp/B07B9F83WM)提供了对需要 2 倍团队/产品交付能力的能力的观点。DiffBlue 是[容量 4，测试自动化](https://devops-research.com/assets/accelerate-book-excerpt.pdf)解决方案的一部分。 [DORA DevOps 现状](https://cloudplatformonline.com/rs/248-TPC-286/images/DORA-State%20of%20DevOps.pdf)也与 DiffBlue 有关，高/更高绩效者进行的手动测试比中/低绩效者少得多。

～由 mdavey 于 2019 年 2 月 13 日发布。

发表在[未分类](https://mdavey.wordpress.com/category/uncategorized/)
