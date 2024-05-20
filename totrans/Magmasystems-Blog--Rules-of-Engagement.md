<!--yml
category: 未分类
date: 2024-05-18 05:21:35
-->

# Magmasystems Blog: Rules of Engagement

> 来源：[http://magmasystems.blogspot.com/2006/03/rules-of-engagement.html#0001-01-01](http://magmasystems.blogspot.com/2006/03/rules-of-engagement.html#0001-01-01)

**My Expectations from a Client**

My first engagement with Finetix has just ended, and it was an eye-opener in certain respects.

I have been thinking about what I would like to include in a retrospective to the client in order to help them manage future projects successfully. Instead of enumerating what I consider to be the positives and negatives of the project, I would like to add some of the aspects to my master “Lessons Learned” list, and also to reiterate some of my long-standing project-management processes.

1) Clearly Define Roles

2) Always Be Engaged

3) Make Sure Everyone Knows Everything

4) Define A Methodology And Stick To It

5) Have The Environment Completely Set Up

6) Have Documentation Ready

7) Engage the Business Analysts and Business Users

8) Do Not Pair-Program Unless Absolutely Necessary

9) Always Have a Roadmap For Refactoring

**Clearly Define Roles** 

If you are bringing in consultants to lead the technical team, then tell your team members and enforce the leadership. If you are expecting your consultants to be short-term body-shoppers who are coding, then tell them this up front. Do not allow incorrect perceptions to pervade the group.

There will always be bruised feelings when you bring consultants on to a project in a leadership role. We consultants completely understand this. Nobody wants their work to be reevaluated and critiqued. If the consultants are being brought in to do rearchitecture, then they must be given the power to lead the effort.

***Make it clear as to who holds the trump card.*** **Always Be Engaged** 

As a project manager, make sure that you know what all of your team members are doing, and make sure that all team members know what each other is doing. Make sure that the server side and client side teams communicate. Many server-side devs have also done GUI work and vice-versa.

If you have to support a legacy version of your product, then make sure that you are able to delegate that task to certain members of the team. Have a plan to get these “legacy developers” involved with the new development. The legacy devs are subject matter experts who are important to the whole team.

**Make Sure Everyone Knows Everything** 

As mentioned above, do not isolate the groups. Involve the Business Analysts and Business Users where appropriate. Unless there are well-defined isolation layers, make sure that you try to completely define the communication layers and formats between the client and server. If the BA’s are planning something new, have them run it by the entire team so that the team can discuss the ramifications on the architecture.

**Define A Methodology And Stick To It** 

If you are going to do Agile or Scrum, then stick to it. If you are going to do Waterfall, then stick to it. If you are going to decide on daily standups, then stick to it.

**Have The Environment Completely Set Up** 

Consultants get paid a lot of money, and their efforts are usually time-boxed. So, make sure that they are productive from day one. Have all user accounts set up. Have all of the software ready. If this software requires additional registration, then make sure that this is done. Make sure that there are enough licenses for the software, and make sure that support packages have been purchased.

Make sure that the computers have enough memory and enough free disk space. Developers need about 2gb of RAM and about 100gb of free hard drive space. Make sure that certain shared drives can be accessed.

Make sure that the security people in the building know that a team is starting, and to expect them. If a consultant is made to wait in the lobby while security tries to track down someone to sign them in, then this serves nobody.

**Have Documentation Ready** 

Does the system have documentation? Use cases? Architecture docs? If not, then either prepare them or prepare for a steeper learning process.

**Engage the Business Analysts and Business Users** 

I have talked about this before. If you are writing a trading system, then the developers should be able to have access to the traders. The developers should be able to peek over a trader’s shoulder while he is working. The developers should have a complete feel for the kind of system that a trader would like to have.

If there are BAs that the developers must interact with, then make sure that the devs and BAs have constant interaction. Make sure that the BAs know if some of their ideas will be difficult to implement.

**Do Not Pair-Program Unless Absolutely Necessary** 

I continue to abhor pair programming. I think that it cuts down productivity in a big way. I think that the best development is done when the developer is “in the zone”, and does not have to expend energy explaining every move to someone else.

Instead, have design meetings and developer meetings. It does not have to be “Big Design Up Front”. However, if a developer is architecting a crucial module, then let him present the design to the entire team and get critiques before the effort is too far gone.

**Always Have a Roadmap For Refactoring** 

Do you know why a product is being refactored? Does the business absolutely need it? Do you really need to rewrite an entire application from scratch?

Remember that, when you refactor an application, you need a plan to retain all of the business logic that is built in to the existing app.

Make sure that the code has comments. Make sure that there is plenty of technical documentation. Make sure that all of the business rules are documented.

Make sure that all dead code has been eliminated from the application. It is difficult to rearchitect a system if the hands of 30 different people have been in it over the years.

These are my ideal Rules of Engagement for any project that I will be on, either as a leader or as a hired hand. I would love to hear your comments.

©2006 Marc Adler - All Rights Reserved