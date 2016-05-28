# LARVARUM COMPUTATIONIS EXAMEN II

OUTLINE OF THE LICENSE, INSTALLATION AND USAGE OF LARVARUM COMPUTATIONIS EXAMEN II



LICENSE:

NAME: LARVARUM COMPUTATIONIS EXAMEN II (LarCom EII)
Copyright (C) 2016 Nino Ivanov kedalion.daimon(-at-)gmail.com

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

See <http://www.gnu.org/licenses/>.

Language: modern Fortran (I used gfortran and g95)
Environment tested: Scientific Linux 6



INSTALLATION AND USAGE

CONTENTS:

I. Introduction
II. Theory
III. Interaction
IV. Operation
A. Prerogatives
B. Directory
C. Compilation
D. Executability
E. Scripts
F. Action
G. Contact



I. Introduction

This is a swarm intelligence operating by means of logical triangulation.

It works as a "chatbot"; however, this is actually a generally intelligent entity. It "learns" from conversing with you. It is very experimental... you have been warned. RESPONSES OF THE SYSTEM CAN TAKE BETWEEN A FEW MINUTES AND A FEW HOURS, TYPICALLY.



II. Theory

The idea is: a general intelligence should apply experience from the past to experiences in the future. To do this, my approach assumes the entire knowledge about the world comes from patterns of perception - and indeed, nothing more. It employs a certain method how to identify and correlate patterns which I name "logical triangulation". The method is symbolic and employs an own new kind of pattern logic - not neural nets, not statistics, not predicate calculus. - The main idea is, "that what is most usual is the most proper reply".

For details of the theoretical background see:

https://sites.google.com/site/logicaltriangulation/

and

https://www.youtube.com/playlist?list=PLZwimPIVfsoN2wBdZvwtAURyQg1jY7upA

Three approaches will be presented (Scheme, Fortran and Common Lisp). The approaches presented here differ in one point: will they employ "instincts" - which are very primitive and just replace "me" with "you", "mine" with "yours" etc. 



III. Interaction

Basically, you will end up in front of a sort of prompt. You will be able to write sentences and the machine will answer you. (In the background, it will attribute the present stage of the conversation to an "insect" in a "swarm" that will be tasked replying to you. The paucity of insects is only for the purpose of demonstration - in reality, you may wish to run it with myriads of insects, if you own a supercomputer...)

It may look something like this - where "READ" shows the human input, "REPLY" shows the machine information, and the ::-lines show some processing information regarding the insects used:

./overlord.sh
 :: SYSTEM OPERATIONAL. ENTER AN EMPTY LINE TO TERMINATE. :: 
READ: hail thee hail thee hail thee
 :: FORCING CONSIDERATION WITH 24 EX 1 :: 
 :: MATCHING MACHINE :: 24
REPLY:  HAIL THEE
READ: Is it actually possible to talk to you? Are you aware of anything?
 :: FORCING CONSIDERATION WITH 23 EX 24 :: 
 :: MATCHING MACHINE :: 23
REPLY:  ARE YOU
READ: I am aware of your presence here, as well as of your experimental nature. I wish to see what you do...
 :: FORCING CONSIDERATION WITH 22 EX 23 :: 
 :: MATCHING MACHINE :: 22
REPLY:  HERE
READ: what is here?
 :: MATCHING MACHINE :: 22
REPLY:  HERE?
READ: Yes, here. What are you even talking about? How do you evaluate things?
 :: FORCING CONSIDERATION WITH 21 EX 22 :: 
 :: MATCHING MACHINE :: 21
REPLY:  ,
READ: Ah, just a comma as a reply does not suffice. Shall we play a game? 
 :: FORCING CONSIDERATION WITH 20 EX 21 :: 
 :: MATCHING MACHINE :: 20
REPLY:  ,
READ: I dont want some ",", I demand a reply! I am thy human overlord!
 :: FORCING CONSIDERATION WITH 19 EX 20 :: 
 :: MATCHING MACHINE :: 19
REPLY:  ,", I DEMAND A REPLY! I AM THY HUMAN
READ: 
 :: EMPTY INPUT. INTERACTION TERMINATED. :: 

Empty input (i.e. just hitting "Enter") will terminate the conversation. (Note: there seems to be some bug if the input is just one word... well... "do not do this".)



IV. Operation

A. Prerogatives

I am assuming you are running some sort of Unixoid (no love for Windows here), and I advise you to check the paths and the programs in overlord.sh, testwords.sh, soloqueen.sh and relink.sh. I have tested this just on Scientific Linux 6, but I did not use anything "fancy" of which I know that it would prevent operation in FreeBSD, NetBSD, OpenBSD or Mac OS X. If you discover the need for any adaptations, it would be kind if you could let me know.

You need a Fortran-compiler, too. (Examples will be given for Gfortran.)



B. Directory

Create an empty directory with a name of your choice, like "larvae" or something.



C. Compilation

In order to eat a hare, you will have to catch one, and in order to run a compiled program, you will have to ... compile something, right?

1. Copy to the directory the file:

pter*.f95

(As of this writing, this is: pter20140923.f95)

Compilation will be shown for Gfortran, though I see no reason why you shouldn't be able to use any modern Fortran compiler of your choice



2. Compile pter using Gfortran:

gfortran -o pter pter*.f95

- You will have an executable named "pter" in your directory (of 61KB).



D. Executability

Now I assume you have the compiled program "pter". Copy now all remaining files into the directory that you have chosen as mentioned under IV. B. Make sure the bash-scripts are executable and the programs are executable (which they should be already):

chmod +x pter *.sh



E. Scripts

A bit of an explanation of the scripts should be given, ere we proceed to ... raise the swarm... ;)

1. So far, you have a few executables and set of files, but no swarm yet. The swarm is created by "soloqueen.sh": When soloqueen.sh is run, the "lone queen" creates the "pupae", the actual insect units, copying into each folder the appropriate files, and creating a link to the main swarm executable.

Then you will actually have a "swarm".



2. What if you just tinker with the Fortran code but do not wish to change the entire swarm? Then, if only the swarm executable is to be updated, use relink.sh that just re-creates the links to the newly created swarm executable.



3. How do you use the whole thing? - The main operation is through overlord.sh (calling testwords.sh, which in turn calls pter) which works as follows:

(i) - Input is sent to all insects into each folder and it is checked whether there is a plan - if so, the answer is shown to the user; the chosen answer (from potentially several) is the one of the "most recently used insect" as determined by the (updated) file insects.txt;

(ii) - if there is no answer, then "re-consideration" is forced and its answer - possibly an empty answer - is given to the user.

(iii) - The re-consideration works by, firstly, forgetting the "oldest unused" insect and, secondly, cloning in its place the "most recently used" insect. This clone becomes itself "most recently used" as it is the one which is forced to re-consider the input. - This way, the most recently used insects are "spawned" into slightly mutated versions.



F. Action

No more ado!

Open a terminal and change to your selected directory.

1. Let the queen do her work:

./soloqueen.sh

2. Activate the overlord:

./overlord.sh

3. Type in your message. (Note: If you use a message of just one word as the very first message, it can be buggy, so use a message of at least a few words.) Like:

hail thee hail thee hail thee

4. Wait... (An hour would not be unusual. - In bigger systems, like the fully expanded Scheme system, you will need to wait for a WEEK or longer!)

5. Read the reply (the machine should have deduced that "hail thee" is a proper response), and GOTO 3. The reply will often be empty or nothing - you are, after all, meeting an entity that KNOWS ABSOLUTELY NOTHING YET. It will need considerable patience to teach it to converse. Sometimes, "dropping" the conversation and retrying is the best solution if it behaves strangely. As I said under I., this system is experimental. (In case you are curious "where the knowledge is, have a look at sysarray.txt in any one of the pupae, specifically, those which have been used in interaction. There are always three numbers which symbolize an atom; whether the first two are positive or not signifies the connection type. The first two are the "child" atoms, the final third one is the "superatom".)

6. If you wish to terminate, just issue empty input, i.e. just hit "Enter" as mentioned above under III.

7. If you wish to run this system in the future, just run:

./overlord.sh

from a terminal in the selected directory.



G. Contact

Have fun and let me know what you think:

https://groups.google.com/forum/#!forum/de-larvis-computationis

Finally, I will show you a Scheme-version that is much larger from the knowledge perspecting and that has been learning for a year and a half from books. (Historically, it is the first version made.)

- Nino Ivanov

kedalion.daimon[~at~]gmail.com
