Title: 6.5840 Project
Mapped Topic: Distributed systems labs and schedule
Source URL: https://pdos.csail.mit.edu/6.5840/project.html
Source Type: official_course
Trust Score: 97
Fetched At: 2026-04-17T07:00:45+00:00
Mapped From CSE.md Section: Part 1 / Part 2.E

# Content

Proposals due: |
Mar 20 23:59 |
Code and write-up due: |
May 8 23:59 |
Presentations: |
May 12 in class |

You can either do a final project based on your own ideas,
or [Lab 5](https://pdos.csail.mit.edu/labs/lab-shard1.html).

If you want to do a project, you must get our approval for your idea in advance. You must form a group of 2 or 3 6.5840 students to collaborate on the project. At the end of the term you'll turn in your code and a short write-up describing the design and implementation of your project, and make a short in-class presentation about your work. We'll post the project write-ups and code on the course web site.

Your project should be something interesting and challenging that's closely related to 6.5840 core topics, such as fault tolerance. The project must involve at least as much effort as Lab 5. Below you'll find some half-baked ideas that we think could turn into interesting projects, but we haven't given them too much thought.

There are four concrete steps to the final project, as follows:

- Form a group and decide on the project you would like to work on. Feel free to use Piazza to find group members and discuss ideas. Course staff will be happy to discuss project ideas via e-mail or in person.
-
Flesh out the exact problem you
will be addressing and how you will go about solving it.
By the proposal deadline, you must
submit a proposal (less than a page) describing: your
**group members**list,**the problem**you want to address,**how you plan to address it**, and what are you proposing to**specifically design and implement**. Submit your proposal to Gradescope (to the assignment called "Final Project Proposal") We'll tell you whether we approve, or not, and give you feedback. - Execute your project: design and build something neat!
- Write a document describing the design and implementation of your project, and turn it in along with your project's code by the final deadline. The document should be about 3 pages of text that helps us understand what problem you solved, and what your code does. You can either send the code to the staff list or provide a link to an repository (e.g., on GitHub) in your writeup. The code and writeups will be posted online after the end of the semester.
- Prepare a short presentation about the work that you have done for your final project, and deliver it during the last class meeting.

You should feel free to propose your own project idea. If you'd like some starting points, here are some topics that might (or might not) be worth thinking about.

- Re-implement one of the systems described in the papers discussed in 6.5840.
- Build a high-performance Raft implementation, changing the design as needed.
- Build a distributed, decentralized, fault-tolerant Reddit.
- Build a system for making Node.js applications fault-tolerant, perhaps using some form of replicated execution.
- Add cross-shard atomic transactions to Lab 5, using two-phase commit and/or snapshots.
- Build a data-flow processing system in the style of Google FlumeJava or Spark or Naiad.
- Build a system with asynchronous replication (like Dynamo or Ficus or Bayou). Perhaps add stronger consistency (as in COPS or Walter or Lynx).
- Build a file synchronizer (like
[Unison](http://www.cis.upenn.edu/~bcpierce/unison/)or[Tra](http://swtch.com/tra/)). - Build a coherent caching system for use by web sites (a bit
like memcached), perhaps along the lines of
[TxCache](http://drkp.net/papers/txcache-osdi10.pdf). - Build a distributed cooperative web cache, perhaps along
the lines of
[Firecoral](https://www.usenix.org/legacy/events/iptps09/tech/full_papers/terrace/terrace_html/)or[Maygh](http://www.ccs.neu.edu/home/amislove/publications/Maygh-EuroSys.pdf). - Build a collaborative editor like EtherPad, using eventually-consistent or CRDT primitives.
- Use a block-chain to build something other than a crypto-currency.
- Build a fault-tolerant and/or sharded file service.
- Build a
[distributed shared memory](https://crystal.uta.edu/~kumar/cse6306/papers/17.pdf)(DSM) system, to make it possible to run existing parallel code intended for a single multi-core machine, but on a cluster of machines. - Build a distributed block store in the style of Amazon EBS or FAB. Maybe you can get standard operating systems to talk to you network virtual disk using iSCSI or Linux's NBD (network block device).
- Build a geo-replicated storage system, like Dynamo or COPS, perhaps providing something useful and/or efficient in the the way of transactions or consistency.
- Use modern high-speed NIC features (e.g. RDMA or DPDK) to build a high-speed service, perhaps with replication or transactions.
- Use modern fast non-volatile storage (e.g. Intel Optane) to simplify the design of a fault-tolerant system.
- Build a fault-tolerance framework that's easier than Raft to layer service code on top of.
- Figure how to say something useful about whether applications really need strictly consistent storage, or what the cost in application complexity is of having to use storage with weak consistency.
- Build a data-processing system that is good at both big data (like MapReduce and Spark) and on-line processing (like a key/value store or SQL database).
