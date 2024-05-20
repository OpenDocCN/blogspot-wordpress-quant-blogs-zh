<!--yml
category: 未分类
date: 2024-05-12 19:58:20
-->

# Falkenblog: Decentralized Networks Need Centralized Oracles

> 来源：[http://falkenblog.blogspot.com/2020/04/decentralized-networks-need-centralized.html#0001-01-01](http://falkenblog.blogspot.com/2020/04/decentralized-networks-need-centralized.html#0001-01-01)

I created an open-source contract and web-front-end,

[OracleSwap](http://oracleswap.co/)

, because I want to see crypto move back to its off-the-grid roots. I cannot administer it because I have too many fingerprints on it to benefit directly. OracleSwap is a template that makes it easy for programmers to administer contracts that reference objective outcomes: liquid assets or sports betting. Users create long or short swap (aka CFD) positions that reference a unique Oracle contract that warehouses prices (the prototype references ETH/USD, BTC/USD, and the S&P500). The only users in this contract are liquidity providers, investors, and oracle. The single attack surface is via a conspiring oracle posting a fraudulent price. It contains several innovations, including forward-starting prices (like market-on-close), netting exposure for liquidity providers, and the ability and incentive for cheated parties to zero-out their cheater.

 The White Paper and Technical Appendix describe it more fully, but I want to explain why a centralized, pseudonymous, oracle is better than a decentralized oracle for smart contracts. Many thoughtful crypto leaders believe decentralization is a prerequisite for any dapp on the blockchain, which they define as implying many agents and a consensus mechanism. This is simply incorrect, a category error that assumes the parts must have all the characteristics of the whole. The bottom line is that decentralized oracles are inefficient and distract from the fundamental mechanism that makes any oracle 'trustless.'

###  Attack and Censorship Resistance Is the Key 

After the first crusade (1099), the Knights Templar safeguarded pilgrims to newly conquered Jerusalem and quickly developed an early international bank. A pilgrim could deposit money or valuables within a Templar stronghold and receive an official letter describing what they had. That pilgrim could then withdraw cash along the route to take care of their needs. By the 12th century, depositors could freely move their wealth from one property to the next.

 The Templars were not under any monarch's control, and even worse, many owed them money. Eventually, King Philip IV of France seized an attack surface by arresting hundreds of top Templars, including the Grand Master, all on the same day across Europe in 1307\. They were charged with heresy, the medieval version of systematic risk, a clear threat to all that is good and noble. A few years later many Templars were executed and the Templar banking system disappeared [unknown Templars were somehow able to flee with their vast fortune, which back then was not digital, and it is a mystery where it went].

 Governments, exchanges, and traditional financial institutions have always fought anything that might diminish their market power. Decentralization is essential for resisting their inevitable attacks, in that if someone takes over an existing blockchain, it can reappear via a hard fork. The present value of the old chain would create a willing and able army of substitute miners if China or Craig Wright decided to appropriate 51% of existing Ethereum miners.

 Vitalik Buterin nicely describes this resiliency in his admirable assessment of his limited power:

> The thing with developers is that we are fairly fungible people. One developer goes down, and someone else can keep on developing. If someone puts a gun to my head and tells me to write a hard fork patch, I'll definitely write the hard fork patch. I'll write the GitHub issue, I'll write up the code, I'll publish it, and I'll do everything they say. If I do this and publish a hard fork patch to delete a bunch of accounts, how many people will be willing to download the update, install it and switch to that update? This is called decentralization.

 Vitalik Buterin.

[TechCrunch: Sessions Blockchain 2018](https://cryptoslate.com/buterin-ethereum-cant-be-forced-to-adopt-code-i-write-merit-of-decentralization/)

Zug, Switzerland

The potential for a hard fork in the case of an attack is the primary protection against outsiders. This depends on the protocol having a deep and committed set of users and developers who prioritize essential bitcoin principles--transparency, immutability, pseudonymity, confiscation-proof, and permissionless access--and why decentralization is critical for long-run crypto security.

 Outside attacks have decimated if not destroyed several once useful financial innovations. E-gold, Etherdelta, Intrade, and ShapeShift all had conspicuous centralization points, allowing authorities to prosecute, close, or force them to submit to traditional financial protocols. A pseudonymous oracle running virtually scripts on remote servers across the globe would be impervious to such interference. This inheritance is what makes Ethereum so valuable, in that dapps do not need their own decentralized consensus mechanisms to avoid such attacks.

 Any oracle that facilitates derivative trading or sports betting is subject to regulation in most developed countries. Dapp corporations are conspicuous attack surfaces. To the extent Augur and 0x do not compete with traditional institutions, authorities are wise to see them as insignificant curiosities simply. If these protocols ever become competitive with conventional financial institutions—by providing a futures position on the ETH price, for instance—all the traditional fiat regulations will be forced upon them under the pretext of safeguarding the public.

[Maker](https://www.reddit.com/r/MakerDAO/comments/de0sys/kyc_is_absolutely_not_acceptable_for_makerdao/)

and

[Chainlink](https://twitter.com/LINKNewsOracle/status/1237920824524443648)

are already flirting with

[KYC](https://en.wikipedia.org/wiki/Know_your_customer)

, because they know they cannot conspicuously monetize markets that will ultimately generate profits without surrendering to the Borg collective.

 Satoshi needed to remain anonymous at the early stages of bitcoin to avoid some local government prosecuting him before bitcoin could work without him. The peer-to-peer system bitcoin initially emulated, Tor, is populated by people who do not advertise on traditional platforms, have institutional investors, or speak at conferences. Viable dapps should follow this example and focus less on corporatization and more on developing their reputation among current crypto enthusiasts.

### Conspiracy-Proofness is Redundant and Misleading 

For cases involving small sums of money, it is difficult for random individuals in decentralized systems to collude at the expense of other participants. The costs of colluding are too high, which eliminates the effect of trolls and singular troublemakers. Yet this creates a dangerous sense of complacency as any robust mechanism must incent good behavior even if there is collusion. If we want the blockchain to handle real, significant transactions someday, this implies cases where there would be enough ETH at stake to presume someone will eventually conspire to hack the system.

Satoshi knew that malicious collusion would be feasible with proof-of-work, just not problematic because it would be self-defeating. In the Bitcoin White Paper, Satoshi emphasized how proof-of-work removed the need for a trusted third party, why the term trustless is often attributed to a decentralized network. With proof-of-work, it is not impossible to double-spend, just contrary to self-interested rationality. Specifically, he wrote that anyone with the ability to double-spend 'ought to find it more profitable to play by the rules … than to undermine the system and the validity of his own wealth.'

 For the large blockchains like Ethereum and Bitcoin, one needs specialized mining equipment that is only valuable if miners follow the letter and spirit of their law. The capital destroyed by manipulating blocks is a thousand-fold greater than the direct hash-power cost of such an attack. While a handful of Bitcoin or Ethereum mining groups can effectively collude and control 51% network control, it is not worrisome because it would not be in their self-interest to engineer a double-spend given the cost of losing future revenue. For example, in the spring of 2019, the head of Binance, Changpeng Zhao, suggested a blockchain rollback to undo a recent theft. The bitcoin community mocked him, and he quickly recanted because this would not be in the long-term self-interest of the bitcoin miners or exchanges. Saving $40 million would decimate a $100 billion blockchain, making this an easy decision.

 People often mention 'collusion resistance' as a primary decentralization virtue. A better term would be 'conspiracy resistance.' A decentralized system must generate proper incentives even if there is collusion because collusion is invariably possible as, in practice, large decentralized blockchains are controlled by a handful of teams (

[Michels' Iron Law of Oligarchy](https://en.wikipedia.org/wiki/Iron_law_of_oligarchy)

). There have been several instances of benign blockchain collusion, which when applied judiciously and sparingly increases resiliency (e.g., vulnerabilities in Bitcoin were patched behind the scenes in September 2018, the notorious Ethereum 2016 rollback in response to the DAO hack). Law professor Angela Walsh

[highlighted](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3326244)

episodes of benign collusion as evidence the Bitcoin and Ethereum are not decentralized, and thus should be more regulated by the standard institutions.

 Lawyers are keen on technical definitions, but the key point is that the conventional regulators cannot regulate Bitcoin or Ethereum if they tried, highlighting the essential decentralization of these protocols. If the SEC in the US, or the FCA in the UK, tried to aggressively regulate Ethereum they would find the decision-makers soon outside their jurisdiction, Similarly, if Joe Lubin and Vitalik Buterin agreed to fold Ethereum into Facebook miners would fork the old chain and the existing Ether would be more valuable on this new chain. To the extent such a move is probable, the protocol is decentralized, safe from outsiders who do not like its vision for whatever reason.

 Conspiracy resistance all comes down to incentives, making sure that those running the system find running the system as generally understood more valuable than cheating. This same profit-maximizing incentive not only keeps miners honest, but it also protects them from themselves. While blockchains have many things in common, they have very different priorities. Users who prioritize speed prefer EOS; those who prioritize anonymity, Monero; institutional acceptance, Ripple. A quorum of miners who conspire to radically change their blockchain's traditional priorities will devalue their asset by alienating their base, and those who share the new priority will not switch over, but rather highlight that their favorite blockchain has been right all along. Competition among cryptos prevents hubristic insiders from doing too much damage.

###  Costly Decentralization 

Quick and straightforward monitoring is essential for creating an incentive-compatible mechanism. For a decentralized oracle, various subsets of agents are at work on any outcome. It is difficult to find a concise set of data on, say, the percentage and type of Augur markets declared invalid, or a listing of Chainlink's past outcome reports. While all oracle reporting exists (immutably!), putting this together is simply impractical for an average user. Further, past errors and cheats are dismissed as anomalies, which lowers the cost of cheating.

 The 2017 ICO bubble encouraged everyone in the crypto space to issue tokens regardless of need; how a token would make a dapp more efficient was a secondary concern for investors eager to invest in the next bitcoin. Even if a small fraction of ICO money was applied to research and development, that implies hundreds of millions of dollars of talent and time focused on creating decentralized dapps that could justify their need for tokens. All would have all recognized the value of a dependable decentralized oracle, yet they were unable to deliver one, a telling failure. The most popular oracles today are effectively centralized, as ChainLink and MakerDAO have conspicuous attack surfaces as they are both tightly controlled by insiders. They will continue to be effectively centralized because the alternative would be an Augur-like system that is intolerably inefficient (slow, hackable, lame contracts).

 Decentralized oracles that depend on the market value of their tokens incenting good behavior have a significant wedge between how much users must pay the oracle and how much is needed to keep it honest. For example, suppose there is a game such that one needs to pay the reporter 1 ETH so that the net benefit of honestly reporting is greater than a scam the reporter can implement. If only 2% of token holders report on an outcome, this implies we must pay 50 ETH to the oracle collectively (1/0.02), as we have no way to focus the present value of the token onto the subset of token-holders reporting. One could force the reporter to post a bond that would be lost if they report dishonestly, but to make this work it would caps payoff at trivial levels based on reporter capital, which inefficiently ignores the present value of the oracle, and also implies a lengthy delay in payment.

 Another problem with decentralized oracles is they generally serve a diverse set of games. While this facilitates delusions of Amazon-like generality, it makes specific contracts poorly aligned with oracle incentives. The frequency and the size of the payoff will vary across applications so that an oracle fee incenting honesty at all times will be too expensive for most applications. Efficient solutions minimize contextual parameters, implying the best general solution will be suboptimal for any particular use.

 While there are obvious costs to decentralization within an oracle, there are no benefits if the fundamental censorship/attack resistance requirement is satisfied. The wisdom of the crowd is not relevant for contracts on liquid assets like bitcoin or the S&P500\. A reputation scoring algorithm is pointless because the most obvious risk is an exit scam, which relies on behaving honestly until the final swindle (Bitconnect).

 To align the oracle's payoff space in a cryptoeconomically optimal way, one needs to create an oracle payoff such that the benefit of truthful reporting always outweighs the costs of misreporting. By having the oracle in total control, its revenue from truthful reporting is maximized; by being unambiguously responsible and easy to audit and punish, its costs from misreporting are fully born by the oracle; by playing a specific repeated game, the cost/benefit calculus is consistent each week; by giving a cheated user the ability and incentive to punish a cheating oracle, the cheat payoff minimized. These all lead to the efficiency of a single-agent oracle.

###  Fault Tolerance 

Unintentional errors can come from corrupted sources or the algorithm that aggregates these prices and posts a single price to the contract. We often make unintentional mistakes and rely on the goodwill and common sense of those we do business with to 'undo' those cases where we might have added an extra zero to a payment. Credit cards allow chargebacks, and if a bank accidentally deposits $1MM in your account, you are liable to pay it back. The downside is that this process involves third parties who enforce the rule that big unintentional mistakes are reversible, and this implies they have rights over user account balances.

 In OracleSwap, the oracle contract itself has two error checks within the solidity code. First, if prices move by more than 50% from their prior value, and secondly, if they are exactly the same as their previous value. These constraints catch the most common errors. Off the blockchain, however, is where error filtering is more efficiently addressed in general, and ultimately it should be made into an algorithm because otherwise, one introduces an attack surface via the human who would verify a final report. Thus, using many people to reduce errors just adds back in the more subtle and dangerous source of bad prices. OracleSwap uses an automated pull of prices from several independent sources, over a couple-minute window, and takes the median. As the contract is targeting long-term investors, a median price from several exchanges will have a tolerable standard error; as the precise feeds and exchanges are unspecified, this prevents censorship; as prices a posted during a 1-hour window that precludes trading, it is easy to collect and validate an accurate price.

###  A Market: Competing Centralized Agents 

Decentralizing oracles solves a problem they do not have: attack and censorship resistance. An agent updating an oracle contract only needs access to the internet and pseudonymity to avoid censorship. Given that, the best way to create proper oracle incentives is to create a game where the payoffs for honesty and cheating are well parameterized, and outsiders can easily verify if an agent is behaving honestly. Simplicity is essential to any robust game, and this implies removing parties and procedures.

 Markets are the ultimate decentralized mechanism. It is not a paradox that markets consist of centralized agents as it is often the nature of things that properties exist at lower levels but not higher ones. A decentralized market just needs consumers to have both choice and information, and for businesses to have free entry. Markets have always depended upon individuals and corporations with valuable reputations because invariably quality is difficult to assess, so consumers prefer sellers with good reputations to avoid going home with bad eggs or a car with bad wiring. Blockchains are the best accountability device in history, allowing contracts to create valuable reputations for their administrators while remaining anonymous and thus uncensorable.

 A set of competing contracts is more efficient than generalized oracles designed for unspecified contracts, or generalized trading protocols designed for unspecified oracles. A simple contract tied to an oracle that is 'all-in' creates clear and unambiguous accountability, generating the strongest incentive for honest reporting