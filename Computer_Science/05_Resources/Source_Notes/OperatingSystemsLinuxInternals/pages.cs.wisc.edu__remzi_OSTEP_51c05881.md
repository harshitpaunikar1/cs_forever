Title: Operating Systems: Three Easy Pieces
Mapped Topic: Operating systems fundamentals
Source URL: https://pages.cs.wisc.edu/~remzi/OSTEP/
Source Type: official_open_book
Trust Score: 97
Fetched At: 2026-04-17T06:54:40+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

## Operating Systems: Three Easy Pieces
|
|||
|
Quick:
Welcome to This book
Another way to help the book out: cite it! Here is the
| |||
|
| |||
|
|

**HOMEWORKS:** Some of the chapters have homeworks at the end, which
require simulators and other code. More details on that, including how to find
said code, can be found here: [HOMEWORK](https://pages.cs.wisc.edu/Homework/homework.html)

**PROJECTS:** While the book should provide a good conceptual guide to key
aspects of modern operating systems, no education is complete without
projects. We are in the process of making the projects we use at the
University of Wisconsin-Madison widely available; an initial link to project
descriptions is available here:
[PROJECTS.](https://github.com/remzi-arpacidusseau/ostep-projects) Coming
soon: the automated testing framework that we use to grade projects.

**BOOKS NEWS:** Many small things to move to version 1.10. Track changes: [NEWS](https://pages.cs.wisc.edu/combined.html)

**ACKNOWLEDGEMENTS:** These students have greatly contributed to this
effort, through endless bug reports and other comments. Your name could go
here! (as well as in the printed book): [ERRATA](https://pages.cs.wisc.edu/combined.html)

**OTHER SYSTEMS BOOKS:** Interested in other systems books? Good!
Of course, we assume some background in [The C Programming Language](https://www.amazon.com/gp/product/0131103628/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0131103628&linkCode=as2&tag=opesysthrea0a-20&linkId=RI2L6WG3HGZM2GXG), so that's a good investment. And [Advanced Programming in the UNIX Environment](https://www.amazon.com/gp/product/0321637739/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321637739&linkCode=as2&tag=opesysthrea0a-20&linkId=4HWBBZINQQWXE53A) is a must for any shelf. On top of that, here are some OS books that could be worth your time:
[Operating Systems: Principles and Practice](https://www.amazon.com/gp/product/0985673524/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0985673524&linkCode=as2&tag=opesysthrea0a-20&linkId=POFASX37S5VWSIEH)
-
[Operating System Concepts](https://www.amazon.com/gp/product/1118063333/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1118063333&linkCode=as2&tag=opesysthrea0a-20&linkId=R2SFV7DSLZB2QQIU)
-
[Operating Systems: Internals and Design Principles (8th Edition)](https://www.amazon.com/gp/product/0133805913/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0133805913&linkCode=as2&tag=opesysthrea0a-20&linkId=EODT5LXEBGLNAEDN)
-
[Modern Operating Systems (4th Edition)](https://www.amazon.com/gp/product/013359162X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=013359162X&linkCode=as2&tag=opesysthrea0a-20&linkId=2ERIFG4YNEB5EBGA)
-
[Linux Kernel Development (3rd Edition)](https://www.amazon.com/gp/product/0672329468/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0672329468&linkCode=as2&tag=opesysthrea0a-20&linkId=MGLA6JQCCPYZGUAH)
-
[Understanding the Linux Kernel](https://www.amazon.com/gp/product/0596005652/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0596005652&linkCode=as2&tag=opesysthrea0a-20&linkId=ZHXHBDHWWOM2RNT7)
-
[The Design and Implementation of the FreeBSD Operating System](https://www.amazon.com/gp/product/0321968972/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321968972&linkCode=as2&tag=opesysthrea0a-20&linkId=6MY3PGOP3Q2QMRRV)
-
[Solaris Internals: Solaris 10 and OpenSolaris Kernel Architecture](https://www.amazon.com/gp/product/0131482092/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0131482092&linkCode=as2&tag=opesysthrea0a-20&linkId=XWTFSOQ7HUINMGJ7)
-
[Mac OS X Internals: A Systems Approach](https://www.amazon.com/gp/product/0321278542/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321278542&linkCode=as2&tag=opesysthrea0a-20&linkId=H33SAF42MNIRYKV5)
-
[The Design of the UNIX Operating System](https://www.amazon.com/gp/product/0132017997/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0132017997&linkCode=as2&tag=opesysthrea0a-20&linkId=B3OSA2URU2K3RIJ3)
-
[UNIX: The Textbook](https://www.amazon.com/gp/product/1482233584/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1482233584&linkCode=as2&tag=opesysthrea0a-20&linkId=f54001cddb37a437a0d9781fb7442e6e)
-
[The Linux Programming Interface: A Linux and UNIX System Programming Handbook](https://www.amazon.com/gp/product/1593272200/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1593272200&linkCode=as2&tag=opesysthrea0a-20&linkId=Y2R2H2YXMB3TI6PO).

**OTHER BOOKS:** So you're looking down here? Well, how about reading something other than tech books all day long? Honestly, you need to be more balanced. Here are some awesome books you should most definitely read. Fiction:
[Cloud Atlas: A Novel](https://www.amazon.com/gp/product/0375507256/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0375507256&linkCode=as2&tag=opesysthrea0a-20&linkId=ZKZAMFQCTL7SZ3KR)
-
[Life of Pi](https://www.amazon.com/gp/product/0156027321/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0156027321&linkCode=as2&tag=opesysthrea0a-20&linkId=DCVISEJESZUDI5GF)
-
[A Prayer for Owen Meany: A Novel](https://www.amazon.com/gp/product/0062204092/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0062204092&linkCode=as2&tag=opesysthrea0a-20&linkId=EUZKNMY6PPYANPEK)
-
[All the Light We Cannot See](https://www.amazon.com/gp/product/1476746583/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1476746583&linkCode=as2&tag=opesysthrea0a-20&linkId=HUYV4U64776LR6FB)
-
[The Book Thief](https://www.amazon.com/gp/product/0375842209/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0375842209&linkCode=as2&tag=opesysthrea0a-20&linkId=X67UQJXUD6RCI5T5)
-
[The Fault in Our Stars](https://www.amazon.com/gp/product/014242417X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=014242417X&linkCode=as2&tag=opesysthrea0a-20&linkId=E7JAOXWAMKPGSEB2)
-
[Tenth of December: Stories](https://www.amazon.com/gp/product/0812984250/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0812984250&linkCode=as2&tag=opesysthrea0a-20&linkId=63XH2LT6KCJXHDC5)
-
[If I Don't Six](https://www.amazon.com/gp/product/0385491204/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0385491204&linkCode=as2&tag=opesysthrea0a-20&linkId=J3OD3MXBDFGP7FOW)
-
[A Game of Thrones](https://www.amazon.com/gp/product/0553593714/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0553593714&linkCode=as2&tag=opesysthrea0a-20&linkId=ZAYNNMPXWOQ45CG3)
-
[To Kill a Mockingbird](https://www.amazon.com/gp/product/0446310786/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0446310786&linkCode=as2&tag=opesysthrea0a-20&linkId=DR72JNDRE3IZWMR2)
-
[The Kite Runner](https://www.amazon.com/gp/product/159463193X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=159463193X&linkCode=as2&tag=opesysthrea0a-20&linkId=NP3ABJBE6ZLRFZRO)
-
[Ender's Game](https://www.amazon.com/gp/product/0812550706/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0812550706&linkCode=as2&tag=opesysthrea0a-20&linkId=TUXVKMYJBOWFQ6GI)
-
[Foundation](https://www.amazon.com/gp/product/0553293354/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0553293354&linkCode=as2&tag=opesysthrea0a-20&linkId=BZRQNNMXD6BFTQRF)
-
[Slaughterhouse-Five](https://www.amazon.com/gp/product/0440180295/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0440180295&linkCode=as2&tag=opesysthrea0a-20&linkId=E7N2DABAVHT6MXT3)
-
[The Shadow of the Wind](https://www.amazon.com/gp/product/0143034901/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0143034901&linkCode=as2&tag=opesysthrea0a-20&linkId=BSPDO76HKZB5LT4W)
-
[Flowers for Algernon](https://www.amazon.com/gp/product/0156030306/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0156030306&linkCode=as2&tag=opesysthrea0a-20&linkId=XU3EKPFEOI6ULFAR)
-
[Holes](https://www.amazon.com/gp/product/0440414806/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0440414806&linkCode=as2&tag=opesysthrea0a-20&linkId=CLPO7NMAVGGTNI7C)
-
[Atonement](https://www.amazon.com/gp/product/038572179X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=038572179X&linkCode=as2&tag=opesysthrea0a-20&linkId=ZRFZTJEPNC2BCWIN)
-
[The Name of the Wind](https://www.amazon.com/gp/product/0756404746/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0756404746&linkCode=as2&tag=opesysthrea0a-20&linkId=MFUPAT7DB3ID2TVG)
-
[Beloved](https://www.amazon.com/gp/product/1400033411/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1400033411&linkCode=as2&tag=opesysthrea0a-20&linkId=QI6FFIOEP7YK5C6R)
-
[For Whom the Bell Tolls](https://www.amazon.com/gp/product/0684803356/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0684803356&linkCode=as2&tag=opesysthrea0a-20&linkId=QILLNCSDWW7NM2GF)
-
[Different Seasons](https://www.amazon.com/gp/product/0451167538/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0451167538&linkCode=as2&tag=opesysthrea0a-20&linkId=S2SO354RYWWOH6MJ)
-
[Neuromancer](https://www.amazon.com/gp/product/0441569595/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0441569595&linkCode=as2&tag=opesysthrea0a-20&linkId=BXUPQGVZQDL6SNFH)
-
[Snow Crash](https://www.amazon.com/gp/product/0553380958/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0553380958&linkCode=as2&tag=opesysthrea0a-20&linkId=7L2HQZ5USYCUPIZZ)
-
[Cryptonomicon](https://www.amazon.com/gp/product/0060512806/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0060512806&linkCode=as2&tag=opesysthrea0a-20&linkId=TKMYZAAGUV6VU3KF)
-
[Shantaram](https://www.amazon.com/gp/product/0312330537/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0312330537&linkCode=as2&tag=opesysthrea0a-20&linkId=XDUPUXQUV6QOC6TP)
-
[A Room with a View](https://www.amazon.com/gp/product/1482694573/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1482694573&linkCode=as2&tag=opesysthrea0a-20&linkId=QMZYOO6EJR34HFSH)
-
[Jude the Obscure](https://www.amazon.com/gp/product/0486452433/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0486452433&linkCode=as2&tag=opesysthrea0a-20&linkId=OIDTUB73NH5CWWKJ)
-
[Illusions: The Adventures of a Reluctant Messiah](https://www.amazon.com/gp/product/0099427869/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0099427869&linkCode=as2&tag=opesysthrea0a-20&linkId=ZTNT7TLXPZLP3YTX)
-
[A Canticle for Leibowitz](https://www.amazon.com/gp/product/0060892994/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0060892994&linkCode=as2&tag=opesysthrea0a-20&linkId=OR3U64T2O6OOET2P)
-
[A Wizard of Earthsea](https://www.amazon.com/gp/product/0547773749/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0547773749&linkCode=as2&tag=opesysthrea0a-20&linkId=KY5VBA26NSCNYG4I)
-
[Black Swan Green](https://www.amazon.com/gp/product/0812974018/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0812974018&linkCode=as2&tag=opesysthrea0a-20&linkId=B4ASBCYQZR2FE2V4)
-
[The Stars My Destination](https://www.amazon.com/gp/product/1876963468/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1876963468&linkCode=as2&tag=opesysthrea0a-20&linkId=TRC25Z25YDU3TGVE)
-
[Ancillary Justice](https://www.amazon.com/gp/product/031624662X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=031624662X&linkCode=as2&tag=opesysthrea0a-20&linkId=AWAQS2EEBXDJKV4W)
-
[My Brilliant Friend](https://www.amazon.com/gp/product/1609450787/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1609450787&linkCode=as2&tag=opesysthrea0a-20&linkId=ZG7EZNINJKMGDIZL)
-
[Crossing to Safety](https://www.amazon.com/gp/product/037575931X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=037575931X&linkCode=as2&tag=opesysthrea0a-20&linkId=DAJ6DDTEWZSPV377)
-
[Possession](https://www.amazon.com/gp/product/0679735909/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0679735909&linkCode=as2&tag=opesysthrea0a-20&linkId=SKHEFHUKOXPBURGF)
-
[The Selected Works of T.S. Spivet](https://www.amazon.com/gp/product/0143117351/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0143117351&linkCode=as2&tag=opesysthrea0a-20&linkId=57FHOLM4SLTAFU3R)
-
[Essential Ellison](https://www.amazon.com/gp/product/0962344745/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0962344745&linkCode=as2&tag=opesysthrea0a-20&linkId=3L5G7AWS725R3OGQ)
-
[The Demolished Man](https://www.amazon.com/gp/product/1596879882/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1596879882&linkCode=as2&tag=opesysthrea0a-20&linkId=FXUCKXUNNH56MWBD)
-
[ The Nightingale](https://amzn.to/2M1vVRK)
-
[ The Overstory](https://www.amazon.com/Overstory-Novel-Richard-Powers/dp/039363552X/ref=as_li_ss_tl?s=books&ie=UTF8&qid=1533580294&sr=1-1&keywords=the+overstory&linkCode=ll1&tag=opesysthrea0a-20&linkId=1d25c9926098f5f8b27a7e33a2eab965&language=en_US)
-
[ The Windup Girl](https://amzn.to/2nfGQIw)
-
[ The Water Knife](https://amzn.to/2LXiNwV)
Non-fiction:
[Seabiscuit: An American Legend](https://www.amazon.com/gp/product/0449005615/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0449005615&linkCode=as2&tag=opesysthrea0a-20&linkId=TBQJLHAW3ST6Y7K4)
-
[Unbroken](https://www.amazon.com/gp/product/0812974492/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0812974492&linkCode=as2&tag=opesysthrea0a-20&linkId=2RNXXOEYURHDPRYW)
-
[Surely You're Joking, Mr. Feynman!](https://www.amazon.com/gp/product/0393316041/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0393316041&linkCode=as2&tag=opesysthrea0a-20&linkId=2ZT7ZYLZEUPGQXVM)
-
[On Intelligence](https://www.amazon.com/gp/product/0805078533/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0805078533&linkCode=as2&tag=opesysthrea0a-20&linkId=4OVFNPZCWBSSWRTW)
-
[The Language Instinct](https://www.amazon.com/gp/product/0061336467/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0061336467&linkCode=as2&tag=opesysthrea0a-20&linkId=4F2UE5N3ZVWMVBKJ)
-
[Flow](https://www.amazon.com/gp/product/0061339202/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0061339202&linkCode=as2&tag=opesysthrea0a-20&linkId=AUNYVHELQZUQQWEI)
-
[Guns, Germs, and Steel](https://www.amazon.com/gp/product/0393317552/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0393317552&linkCode=as2&tag=opesysthrea0a-20&linkId=GISBBEVE2RUIGPYG)
-
[The Selfish Gene](https://www.amazon.com/gp/product/0199291152/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0199291152&linkCode=as2&tag=opesysthrea0a-20&linkId=6NCHRWJZW24PV5XO)
-
[A Heartbreaking Work of Staggering Genius](https://www.amazon.com/gp/product/0375725784/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0375725784&linkCode=as2&tag=opesysthrea0a-20&linkId=UDMG7GKIKQST3KJE)
-
[Lies My Teacher Told Me](https://www.amazon.com/gp/product/0743296281/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0743296281&linkCode=as2&tag=opesysthrea0a-20&linkId=DZOMLI4INDEJ22FR)
-
[Freakonomics](https://www.amazon.com/gp/product/0060731338/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0060731338&linkCode=as2&tag=opesysthrea0a-20&linkId=FAA3MI6HFRE3T5IS)
-
[How the Irish Saved Civilization](https://www.amazon.com/gp/product/0385418493/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0385418493&linkCode=as2&tag=opesysthrea0a-20&linkId=RBJZ6VWF6GCQ7GDM)
-
[Cod](https://www.amazon.com/gp/product/0140275010/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0140275010&linkCode=as2&tag=opesysthrea0a-20&linkId=U3HIG4I3BZMEKLJ2)
-
[The Devil in the White City](https://www.amazon.com/gp/product/0375725601/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0375725601&linkCode=as2&tag=opesysthrea0a-20&linkId=TXNICNDRY7INUZTQ)
-
[The Swerve: How the World Became Modern](https://www.amazon.com/gp/product/0393343405/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0393343405&linkCode=as2&tag=opesysthrea0a-20&linkId=3LQOCO3VMY3EALMA)
-
[The Drunkard's Walk](https://www.amazon.com/gp/product/0307275175/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0307275175&linkCode=as2&tag=opesysthrea0a-20&linkId=E6LOGFEIWQKDFHCL)
-
[The Visual Display of Quantitative Information](https://www.amazon.com/gp/product/0961392142/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0961392142&linkCode=as2&tag=opesysthrea0a-20&linkId=J7IF4P4ER3NMGP53)
-
[Eats, Shoots & Leaves](https://www.amazon.com/gp/product/1592402038/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1592402038&linkCode=as2&tag=opesysthrea0a-20&linkId=BBGKEIX3M7SRN7GM)
-
[The Elements of Style](https://www.amazon.com/gp/product/020530902X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=020530902X&linkCode=as2&tag=opesysthrea0a-20&linkId=WHRCF5SAP7NDMGZQ)
-
[The Design of Everyday Things](https://www.amazon.com/gp/product/0465067107/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0465067107&linkCode=as2&tag=opesysthrea0a-20&linkId=NSXWP7LMX65XSTPW)
-
[Mountains Beyond Mountains](https://www.amazon.com/gp/product/0812980557/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0812980557&linkCode=as2&tag=opesysthrea0a-20&linkId=6VSP3WPAQNHBL3PU)
-
[The Soul of A New Machine](https://www.amazon.com/gp/product/0316491977/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0316491977&linkCode=as2&tag=opesysthrea0a-20&linkId=4A4IJMCTYKYP5LGP)
-
[Alan Turing: The Enigma](https://www.amazon.com/gp/product/069116472X/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=069116472X&linkCode=as2&tag=opesysthrea0a-20&linkId=5T6AXIPMGOWEUJHX)
-
[Consider the Lobster](https://www.amazon.com/gp/product/0316013323/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0316013323&linkCode=as2&tag=opesysthrea0a-20&linkId=YSNPSOPXUODWNN3R)
-
[The Vintage Guide to Classical Music](https://www.amazon.com/gp/product/0679728058/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0679728058&linkCode=as2&tag=opesysthrea0a-20&linkId=YLI7SXJYHMHA6SCU)

**ACKS:** The authors wish to acknowledge all the sources of
funding for their research over the years. In particular, the authors
appreciate the strong support from the [
National Science Foundation (NSF),](https://www.nsf.gov) which is an essential part of the
modern research and educational infrastructure of the USA.

.
