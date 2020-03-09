"Aristotle’s Topics" by Hugh Burns

The story headline is "A Computer-Prompted Invention Program".
The story genre is "Non-Fiction".
The story description is "IF WE TAKE EACH OTHER SERIOUSLY, YOU'LL THINK ABOUT YOUR TOPIC AS YOU NEVER HAVE BEFORE."
The story creation year is 1979.

Release along with a website, an interpreter, and the source text.

Chapter 1 - The old school

[In which we teach Inform how to behave a little more like '70s-era BASIC.]

The Agora is a room. [Inform requires the world to contain at least one room, even though we are not using its world model at all, in the interest of fidelity to the original program.]

Section 1 - Line input

[Curiously, Inform offers no phrases that simply pause in the middle of running code and wait for the user to type something. BASIC has this capability, and the program makes pervasive use of it.]

Include (- Global user_input = 100; -) after "Parser.i6t".

The user input is a snippet that varies. The user input variable translates into I6 as "user_input".

To call KeyboardPrimitive: (-
	KeyboardPrimitive(buffer, parse);
	user_input = 100 + WordCount();
-).

To get a line of input, ignoring blank lines:
	call KeyboardPrimitive;
	if ignoring blank lines:
		while the user input is "":
			call KeyboardPrimitive.

To wait for the user to press Return:
	call KeyboardPrimitive.

To decide whether the user agrees:
	get a line of input;
	if the user input matches the regular expression "YE", decide yes;
	decide no.


Section 2 - Printing

To print (X - some text):
	say fixed letter spacing;
	say X in upper case;
	say variable letter spacing.

To say tab:
	say "              ". [Judging by the transcripts, a tab is fourteen spaces.]


Section 3 - Running the program

[Topoi doesn't use any of Inform's action processing or turn sequence rules. Instead the entire program runs under the "when play begins" rule below.]

When play begins:
	run the introductory sequence;
	while 0 < 1:
		run the main loop.


Chapter 2 - What Is a Question?

[In which we present an unconventional view.]

A question is a kind of object.

A question can be asked or unasked. A question is usually unasked. A question can be explained or unexplained. A question is usually unexplained. [These sentences effectively define two boolean fields on each question, specifying that they are false by default.]

A difficulty is a kind of value. A question has a difficulty. The difficulties are easy and hard. [The program starts with a few softball questions before getting into the tricky stuff.]

Some questions are defined by the Table of Aristotelian Questions.

The current question is a question that varies. [This defines a global variable named "the current question".]


Chapter 3 - Global Variables

[In which we lay out the state of the program.]

The first name is some text that varies. The first name is "Jane".
The last name is some text that varies. The last name is "Bloggs".
The subject is some text that varies. The subject is "Interactive Fiction".
The purpose is some text that varies.
The key point is some text that varies.

The ask count is a number that varies.
The explore count is a number that varies.
The topic change count is a number that varies.

[These variables are reset each time the program asks a new question.]
The unrecognized question count is a number that varies.
The exploration meter is a number that varies.
The ampersand usage flag is a truth state that varies. [It is true if the user used "&&" while answering the current question.]
The something else flag is a truth state that varies.


Chapter 4 - The Program

[In which we reproduce the logic of the original BASIC program.]

Section 1 - Hello And Welcome!

To run the introductory sequence:
	print "[line break][line break][line break][line break][line break][tab]A COMPUTER-PROMPTED INVENTION PROGRAM:[line break][tab]-------------------------------------[line break][line break][tab]          ARISTOTLE'S TOPICS[line break][tab]          ------------------[line break][line break][line break][line break][line break][tab]HELLO AND WELCOME![line break][line break]";
	[00250]
	print "PLEASE TYPE IN YOUR FIRST NAME:  ";
	get a line of input, ignoring blank lines;
	now the first name is the user input;
	[00290]
	print "[line break]NOW, [first name], PLEASE TYPE IN YOUR LAST NAME:  ";
	get a line of input, ignoring blank lines;
	now the last name is the user input;
	[00312]
	[The special input TEST! makes Topoi skip the introductory stuff, ask the first question, and jump to the main loop--without selecting a subject.]
	if the last name is not "TEST!":
		introduce ourselves;
		offer directions;
		offer some background;
		get the initial subject;
		get the user's purpose;
	[03330 'PAGING OPENING QUESTIONING SEQUENCE]
	print "[line break][line break][line break][line break][line break][tab]RELAX NOW, [first name], AND ENJOY THIS BRAINSTORMING SESSION.[line break][line break][line break][line break][line break][line break][line break][line break][line break][line break][line break][line break][line break][line break]";
	ask a question.

To introduce ourselves:
	[00320]
	print "[line break][line break]WELL, [first name] [last name], I HOPE I CAN BE OF SOME ASSISTANCE[line break]TO YOU TODAY.  IF WE TAKE EACH OTHER SERIOUSLY, YOU'LL[line break]THINK ABOUT YOUR TOPIC AS YOU NEVER HAVE BEFORE.[line break][line break][line break][tab]BEFORE WE BEGIN, [first name],  THERE'S AN OLD[line break]SAYING ABOUT COMPUTER-ASSISTED INSTRUCTION,  IT GOES:[line break][line break][tab]'GARBAGE IN, GARBAGE OUT!'[line break][line break]IN OTHER WORDS, YOU AND I MUST WORK TOGETHER SO[line break]YOU CAN GET A GOOD START ON YOUR RESEARCH PAPER.[line break][line break][line break][line break][tab][tab](PRESS 'RETURN' TO CONTINUE.)";
	wait for the user to press Return.

To offer directions:
	[00510]
	print "[line break][line break][line break]WOULD YOU LIKE TO REVIEW THE DIRECTIONS AND THE COMMANDS?[line break][tab](YES OR NO?)[line break]";
	if the user agrees:
		show directions and commands.

To offer some background:
	[01570]
	print "[line break][line break][line break][line break]WOULD YOU LIKE A BRIEF EXPLANATION OF HOW[line break]ARISTOTLE'S TOPICS HELP WRITERS WRITE?[line break][tab](YES OR NO?)[line break]";
	if the user agrees:
		print "[line break][line break][tab]I'M GLAD YOU ASKED, [first name].  BRIEFLY, THE TWENTY-EIGHT[line break]ENTHYMEME TOPICS HELP A WRITER (OR A SPEAKER) DISCOVER[line break]SPECIFIC ARGUMENTS ABOUT SUBJECTS.[line break][line break][tab]IN HIS 'RHETORIC', ARISTOTLE TELLS US THAT THE AIM OR GOAL[line break]OF RHETORIC IS TO PERSUADE AN AUDIENCE.  REMEMBER THAT TERM --[line break]PERSUADE.[line break][line break][tab]ARISTOTLE BELIEVED THAT IF HIS STUDENTS IN THE[line break]ACADEMY KNEW AND PRACTICED USING THE TOPICS, THEY WOULD BECOME[line break]EFFECTIVE 'PERSUADERS.'[line break][line break][tab]YOU'LL RECOGNIZE AMONG THE TOPICS:[line break][line break]";
		print "[tab]1.  QUESTIONS OF DEVINITION;[line break]";
		print "[tab]2.  QUESTIONS ABOUT CAUSES AND EFFECTS;[line break]";
		print "[tab]3.  QUESTIONS REGARDING OPPOSITES AND ASSOCIATIONS;[line break]";
		print "[tab]4.  QUESTIONS ABOUT CONSEQUENCES;[line break]";
		print "[tab]5.  AND QUESTIONS ABOUT MATTERS OF FACT AND OPINION.[line break][line break][tab][tab](HIT 'RETURN' TO CONTINUE.)[line break]";
		wait for the user to press Return.


Section 2 - Directions

To show directions and commands:
	[00600 <<<   DIRECTIONS AND COMMANDS   >>>]
	print "[line break][line break][tab]DIRECTIONS:[line break][line break][line break]";
	print "[tab]1.  WHEN YOU MAKE A TYPING ERROR, [first name], AND[line break][tab]WISH TO CORRECT IT, USE THE 'RUBOUT' OR 'RUB' KEY.[line break][tab]THE 'SHIFT' MUST BE DEPRESSED WHEN YOU 'RUBOUT'.[line break][tab]IT MAY LOOK A LITTLE FUNNY (LIKE WRITING BACKWARDS),[line break][tab]BUT DON'T WORRY; IT WORKS THAT WAY.[line break][line break][line break]";
	print "[tab]2.  REMEMBER THAT I CAN ONLY READ ABOUT A LINE AND[line break][tab]A HALF OF INFORMATION AT ONE TIME -- ABOUT THIS MUCH:[line break][line break]---------------------------------------------------------------------------------------------------------[line break][line break][tab]HIT 'RETURN' AT THAT POINT AND I'LL GENERALLY[line break][tab]LET YOU ADD MORE INFORMATION.  IF THAT DOES NOT WORK,[line break][tab]TYPE '&&' AND I'LL SAY 'GO ON, [first name].'[line break][line break][line break][tab][tab](PRESS 'RETURN' TO CONTINUE.)";
	wait for the user to press Return;
	print "[line break][line break][tab]3.  AFTER YOU FINISH TYPING YOUR RESPONSE, YOU MUST PRESS[line break][tab]THE 'RETURN' KEY.  WHEN YOU DO , I'LL READ YOUR[line break][tab]RESPONSE AND SAY SOMETHING BACK TO YOU.[line break][line break][line break][tab]4.  THE MOST IMPORTANT OBJECTIVE OF THIS PROGRAM[line break][tab]IS TO GET YOU THINKING ABOUT YOUR TOPIC.[line break][line break][tab]IN ORDER TO ACHIEVE THIS OBJECTIVE,[line break][tab]YOU ARE GOING TO HAVE TO FORGET THAT I AM A MACHINE.[line break][line break][tab]PLEASE ASK QUESTIONS.  YOU'LL BE SURPRISED BY HOW MUCH[line break][tab]I KNOW (OR SO I HOPE!)  I'M NOT[line break][tab]GUARANTEEING THE TRUTH, BUT I'LL DO THE BEST I CAN.[line break][tab]MY MEMORY IS STILL DEVELOPING.[line break][line break][line break][line break][tab][tab](HIT 'RETURN' TO CONTINUE.)[line break][line break][line break]";
	wait for the user to press Return;
	[The following lines have just the right numbers of space characters to align the second column when printed in a fixed-width font. This is necessary because [tab] is always a fixed 14 characters in our program; I tried making the "print" rule handle tab characters, but Inform is not well suited to such fine-grained string hackery; it worked but it was too slow.]
	print "[line break][line break][line break][tab]COMMANDS:[line break][line break]";
	print "[tab]TYPE IN-->    I'LL DO THIS-->[line break]";
	print "[tab]----------    ---------------[line break][line break]";
	print "[tab]STOP!         I'LL STOP ASKING QUESTIONS AND CLOSE.[line break][line break]";
	print "[tab]CONTINUE!     I'LL SKIP AHEAD TO THE NEXT QUESTION.[line break][line break]";
	print "[tab]REPEAT!       I'LL REPEAT THE QUESTION.[line break][line break]";
	print "[tab]DIRECTIONS!   I'LL SHOW YOU THE DIRECTIONS AGAIN.[line break][line break]";
	print "[tab]CHANGE!       I'LL LET YOU CHANGE OR NARROW YOUR SUBJECT.[line break][line break]";
	print "[tab]?             I'LL LET YOU ASK A QUESTION.[line break][line break]";
	print "[tab]EXPLAIN!      I'LL EXPLAIN THE QUESTION.[line break]";
	print "[tab]              (THIS ONE IS A LOT OF FUN, [first name].)[line break][line break]";
	print "[tab]&&            I'LL LET YOU CONTINUE WITH YOUR RESPONSE.[line break][line break]";
	print "[tab][tab](PRESS 'RETURN' TO CONTINUE.)";
	wait for the user to press Return;
	print "[line break][line break][line break][line break][tab]TWO LAST THINGS:[line break][line break]";
	print "[tab]***  THINK OF ME AS A PERSON WHO CAN ASK A LOT OF[line break][tab]INTERESTING, THOUGHT-PROVOKING, AND WILD QUESTIONS.[line break][line break][line break]";
	print "[tab]***  SCREAM FOR HELP IF I START ACTING REALLY CRAZY!![line break][line break][line break]".


Section 3 - Getting a subject

To get the initial subject:
	[01930   <<<   SUBJECT SEQUENCE   >>>]
	print "[line break][line break][line break][line break][line break][line break][line break][line break][line break][line break][tab]NOW I NEED TO FIND OUT WHAT YOU[line break]ARE WRITING ABOUT, SO WOULD YOU PLEASE TYPE IN YOUR[line break]SUBJECT.  I AM LOOKING FOR ONE TO THREE WORDS.[line break][line break][line break][line break][line break][line break]";
	input the subject;
	print "[line break][one of]HOLY ELECTRONICS!  THAT'S WEIRD, I USED TO DATE A COMPUTER[line break]INTERESTED IN [the subject].[line break][or]HEY, THAT'S NEAT, [first name]!  WE'LL HAVE A GOOD TIME THINKING[line break]ABOUT [the subject].[or][the subject], MMMMM!  WILL YOU BE AMAZED[line break]BY THE RECENT SCHOLARSHIP.  BE SURE TO ASK THE LIBRARIAN[line break]IN THE REFERENCE AREA.[purely at random][line break]".

To input the subject: [02120]
	while 0 < 1:
		print "[line break][tab]";
		get a line of input, ignoring blank lines;
		now the subject is the user input;
		if the number of characters in the subject < 40:
			break;
		print "[line break]THAT'S A MOUTHFUL, [first name].  MAKE IT SHORTER, LIKE A TITLE.[line break][tab]HERE ARE A FEW EXAMPLES:[line break][line break]";
		print "[tab]  **   THE ENERGY CRISIS[line break]";
		print "[tab]  **   AUSTIN'S HISTORICAL GARDENS[line break]";
		print "[tab]  **   THE BERMUDA TRIANGLE[line break][line break][line break]";
		print "[tab]YOUR TURN.  WHAT IS YOUR SUBJECT?[line break]".


Section 4 - Purpose

To get the user's purpose:
	[02520 <<<   PURPOSE SEQUENCE   >>>]
	print "[line break][line break][line break][line break][line break][tab]A COMMENT ABOUT PURPOSE:[line break][line break][line break][line break][tab]DURING THIS EXPLORATION PROCESS,[line break][tab]YOU WILL BE ASKED TO CLARIFY THE PURPOSE OF[line break][tab]YOUR PAPER ON [the subject].[line break][line break][line break][tab]SO NOW WOULD YOU BRIEFLY DESCRIBE WHAT THE PURPOSE[line break][tab]OF YOUR PAPER BY COMPLETING[line break][tab]THIS STATEMENT:  THE PURPOSE OF THIS PAPER IS TO. . . .[line break][tab](LIMIT:  ONE LINE)[line break][line break][line break]";
	get a line of input, ignoring blank lines;
	now the purpose is the user input;
	print "[line break]";
	ask for any more;
	print "[line break][tab]FINE, [first name], YOU AND I WILL TALK AGAIN ABOUT YOUR[line break][tab]PURPOSE.[line break][line break][line break]".

To revisit the user's purpose:
	[02810 'PURPOSE SUBROUTINE AT C+1=6]
	print "[line break][line break][tab]BEFORE WE CONTINUE, [first name], I WANT YOU[line break][tab]TO THINK ABOUT YOUR PURPOSE ONCE AGAIN.[line break][line break][tab]YOU HAVE ALREADY TOLD ME THAT YOUR PURPOSE WAS[line break]TO [purpose].[line break][line break][line break][tab]HOW WOULD YOU COMPLETE THIS STATEMENT:[line break][line break][tab]IF NOTHING ELSE, I WANT MY READER TO UNDERSTAND. . . .[line break][tab](ONE LINE, PLEASE)[line break][line break][line break]";
	get a line of input, ignoring blank lines;
	now the key point is the user input;
	print "[line break]";
	ask for any more;
	print "[tab]OKAY, FINE.  KEEP YOUR PURPOSE IN MIND AS WE CONTINUE.[line break][line break]".

To revisit the user's purpose again:
	[03060 'PURPOSE SUBROUTINE AT C+1=12]
	print "[line break]";
	[03070   IF N4>0 THEN 3000 -- this is apparently dead code; N4 is not otherwise mentioned.]
	print "[line break][tab]LET'S PAUSE ONCE AGAIN TO CONSIDER YOUR INTENT.[line break][line break][tab]YOUR GENERAL PURPOSE IS TO[line break][purpose][line break][line break][tab]ALSO, YOU WANT YOUR READER TO UNDERSTAND[line break][the key point].[line break][line break][line break][tab]IS THERE ANYTHING ELSE YOU WISH TO SAY ABOUT PURPOSE?[line break][tab][tab](YES OR NO?)[line break]";
	if the user agrees:
		print "[line break][tab]GREAT, [first name], WHAT WOULD YOU LIKE TO ADD?[line break][tab](ONE LINE LIMIT IN EFFECT)[line break][line break][line break]";
		get a line of input, ignoring blank lines;
		ask for any more;
	print "[line break][tab]FINE, [first name], ENOUGH ABOUT PURPOSE.[line break]".

To ask for any more: [03321]
	print "[line break][tab]ANY MORE?[line break][tab](IF SO, TYPE WHATEVER IT IS; IF NOT, TYPE 'NO'.)[line break][line break]";
	get a line of input [which we will ignore];
	print "[line break]".


Section 5 - Asking Questions

To ask a question:
	[03520 <<<   COUNTER/EXPLORATION CONTROLS   >>>]
	increment the ask count;
	if the ask count is greater than 30:
		quit;
	now the exploration meter is 0;
	now the something else flag is false;
	now the unrecognized question count is 0;
	now the ampersand usage flag is false;
	if the ask count <= 5:
		[03570]
		now the current question is a random unasked easy question;
	else:
		[03610 'OPENS TOTAL POOL AFTER FIVE QUESTIONS]
		now the current question is a random unasked question;
	now the current question is asked;
	print the text of the current question.

To repeat the question:
	print "[line break]";
	print the text of the current question [once again].

To move on to the next question:
	print "[line break][line break][tab]HERE IS YOUR NEXT QUESTION -- NUMBER [ask count + 1].[line break][line break][line break]".


Section 6 - Asking More Questions

To decide if the next question will be number (N - a number):
	if the ask count plus one is N, decide yes;
	decide no.

To segue into the next question, maybe offering a subject change:
	if maybe offering a subject change:
		[06180]
		print "[line break]";
		if the next question will be number 3 or the next question will be number 8:
			offer a change of subject;
	[06210]
	if the next question will be number 6:
		revisit the user's purpose;
		move on to the next question;
	else if the next question will be number 12:
		revisit the user's purpose again;
		move on to the next question;
	else:
		print "[line break][line break]";
		choose a random row in the Table of Suggestions;
		print "([suggestion entry])[line break]";
		[06460]
		print "[line break][line break][line break][line break]";
		choose a random row in the Table of Next Question Segues;
		print "[segue entry][line break][line break]";
	ask a question.

Table of Suggestions
suggestion
"SEE IF YOU CAN USE SOME MORE ACTION VERBS IN YOUR RESPONSE."
"REMEMBER NOT TO WORRY ABOUT SPELLING!!"
"I'LL EXPLAIN MORE IF YOU ASK ME ON THIS NEXT QUESTION."
"AFTER I ASK THIS NEXT QUESTION, TYPE 'WHAT?' AND STAND BACK."
"SEE IF YOU CAN USE THE WORD 'BECAUSE' IN YOUR NEXT ANSWER."
"IF YOU DON'T UNDERSTAND, JUST SAY SO NEXT TIME.  I'LL HELP."
"I REPEAT QUESTIONS IF YOU TYPE 'REPEAT!'"
"IF YOU NEED MORE ROOM, TYPE '&&' AT THE END OF A LINE."
"TRY USING SOME MORE VERBS FOR BETTER EXPLANATIONS."
"TRY EXPLAINING A LITTLE MORE.  LESS PHRASES, MORE SENTENCES."

Table of Next Question Segues
segue
"WE'RE MOVING RIGHT ALONG.  HERE IS QUESTION [ask count + 1]."
"AND HERE COMES A REALLY INTERESTING QUESTION -- NUMBER [ask count + 1]."
"QUESTION [ask count + 1] -- ONE OF MY ALL-TIME FAVORITES COMING UP."
"YOUR NEXT QUESTION IS NUMBER [ask count + 1]."
"HERE IS QUESTION [ask count + 1], [first name].";


Section 7 - The Main Loop

The saved input flag is a truth state that varies. The saved input flag is false.

To run the main loop:
	if the saved input flag is true:
		now the saved input flag is false;
	otherwise:
		while 0 < 1:
			print "[line break][line break]";
			get a line of input, ignoring blank lines;
			if the user input matches the text "CONTINUE!":
				segue into the next question, maybe offering a subject change;
			else if the user input is "NO":
				respond to NO after a prompt;
			else:
				break;
	if the user input matches the text "STOP!":
		quit;
	else if the user input matches the text "REPEAT!":
		repeat the question;
	else if the user input is "?":
		let the user ask a question;
	else if the user input matches the text "DIRECTIONS!":
		show directions and commands;
		get back to the questions;
	else if the user input matches the regular expression "HOW.*\?":
		answer a HOW question;
	else if the user input matches the regular expression "WHY.*\?":
		answer a WHY question;
	else if the user input matches the text "&&":
		encourage the user to go on;
	else if the user input matches the text "EXPLAIN!":
		explain the question;
	else if the user input matches the regular expression " DO.*N.*T .*UNDERST":
		explain the question;
	else if the user input matches the regular expression " DO.*N.*T .*KNOW":
		explain the question;
	else if the user input matches the text "CHANGE!":
		change the subject;
		segue into the next question [without offering a subject change, since we just did that];
	else if the user input matches the regular expression "WHAT.*\?":
		explain the question;
	else if the user input matches the regular expression "MEAN.*\?":
		explain the question;
	else if the user input matches the regular expression " OR .*\?":
		answer an OR question;
	else if the user input matches the regular expression "CAN I .*\?":
		answer affirmatively;
	else if the user input matches the regular expression "IS .*IT .*\?":
		answer affirmatively;
	else if the user input matches the text "BECAUSE":
		reward BECAUSE;
		perform exploration branching and feedback, without initial line breaks;
	else if the user input matches the text "?":
		respond to an unrecognized question;
	else if the something else flag is true:
		[06160]
		print "[line break][tab]OKAY.[line break]";
		segue into the next question, maybe offering a subject change;
	else if the ampersand usage flag is true:
		perform exploration branching and feedback;
	else if the number of characters in the user input is less than 10:
		encourage elaboration;
	else if the user input is grandiloquent:
		respond to garbage or jargon;
	else:
		perform exploration branching and feedback.

To get back to the questions [after printing directions]: [01510]
	print "[tab]BACK TO THE QUESTIONS, [first name]   -->   -->   -->[line break][line break][line break][line break][tab][tab]BUT FIRST, IS THERE[line break]";
	ask anything else.

To perform exploration branching and feedback, without initial line breaks:
	[05770 <<<   EXPLORATION BRANCHING AND FEEDBACK   >>>]
	if not without initial line breaks:
		print "[line break][line break]";
	increment the exploration meter;
	if the exploration meter is 1:
		print "[one of]GOOD, [first name], ADD TO YOUR RESPONSE NOW.[or]FINE, [first name].  WRITE SOME MORE.[or]THAT'S THE IDEA, [first name].  GIVE ME SOME MORE INFO NOW.[or]BY GEORGE, [first name], GOOD ONE.  WRITE A LITTLE MORE PLEASE.[purely at random][line break]";
	otherwise:
		print "[one of]SUPER[or]OUTSTANDING[or]FANTASTIC[or]TERRIFIC[or]GREAT[purely at 	random], [first name]![line break][line break]";
		increment the explore count;
		ask anything else.

To ask anything else: [06050]
	print "[tab][tab]ANYTHING ELSE?[line break]";
	if the explore count <= 2:
		print "[tab][tab](YOU CAN ADD MORE INFO, ASK A[line break][tab][tab]QUESTION, OR GIVE A COMMAND --[line break][tab][tab]WHATEVER YOU WISH.)[line break][line break]";
	if the user agrees: [<--- note that this sets "the user input", which is used in the "otherwise:" case]
		[06780 'ANSWERS A *YE* TO ANYTHING ELSE?]
		print "[line break]WHAT?[line break]";
	otherwise:
		now the something else flag is true;
		now the saved input flag is true.

To respond to NO after a prompt:
	[06622 'RESPONDS TO I$=NO AFTER INVENTION PROMPTER]
	print "[line break][tab]YOU COULD TELL ME 'WHY NOT', BUT YOU[line break]MAY JUST WANT TO CONTINUE.  IF SO, TYPE 'CONTINUE![line break](DON'T FORGET THE EXCLAMATION POINT!)[line break]".

To decide if (line - some text) is grandiloquent:
	[05650 'CHECKS LENGTH OF INDIVIDUAL WORDS IN STRING]
	repeat with K running from 1 to the number of unpunctuated words in the line:
		let W be unpunctuated word number K in the line;
		if the number of characters in W is greater than 15:
			decide yes;
	decide no.

To respond to garbage or jargon:
	[06630 'RESPONSE TO 'GARBAGE' OR JARGON]
	print "[line break][tab]HEY, [first name], WHAT KIND OF LANGUAGE IS THAT?[line break][tab]TRY AGAIN. I JUST CAN'T UNDERSTAND WHAT YOU SAID?[line break][line break][tab](YOU MAY HAVE RUN SOME OF YOUR WORDS TOGETHER,[line break][tab]SO IF YOU CAN UNDERSTAND WHAT YOU MEAN, JUST[line break][tab]KEEP ON ANSWERING THE QUESTION.  I'LL REPEAT[line break][tab]THE QUESTION IF YOU TYPE 'REPEAT!')[line break]".

To encourage the user to go on:
	print "[line break]GO ON, [first name].[line break]";
	now the ampersand usage flag is true.

To let the user ask a question:
	[06750 'ANSWERS THE SINGLE QUESTION MARK (I$="?")]
	print "[line break]GO AHEAD, [first name], ASK.  I'LL DO THE BEST I CAN.[line break]".

To answer a HOW question:
	[06810 'ANSWERS THE QUESTION *HOW*?*]
	print "[line break]I COULD SAY THAT THAT'S FOR ME TO KNOW AND FOR YOU TO FIND OUT.[line break][line break]SERIOUSLY, I CANNOT PRETEND TO KNOW 'HOW', BUT YOU[line break]SHOULD KEEP EXPLORING FOR AN ANSWER.[line break][line break]".

To answer a WHY question:
	[06880 'ANSWERS THE QUESTION *WHY*?*]
	print "[line break]WELL, WHY NOT?  REMEMBER WE ARE EXPLORING, BRAINSTORMING![line break][line break]".

To change the subject:
	[06920 'ANSWERS THE *CHANGE!* COMMAND]
	print "[first time][line break]GOOD FOR YOU, [first name].  NOT EVERY WRITER NARROWS OR[line break]CHANGES HIS OR HER TOPIC THIS EARLY IN THE INVENTION PROCESS.[line break][only]";
	print "[line break]PLEASE TYPE IN YOUR NEW SUBJECT:[line break]";
	input the subject;
	print "[line break]YOUR REVISED SUBJECT IS [the subject].[line break][line break][line break][line break][line break][line break]".

To answer an OR question:
	[07000 'ANSWERS QUESTION * OR *?*]
	print "[line break]WHATEVER YOU THINK BEST, [first name].  YOU DECIDE.[line break][line break]";

To answer affirmatively:
	[07040 'ANSWERS QUESTION *CAN I *?*]
	print "[line break]YES, OF COURSE.[line break][line break]".

To reward BECAUSE:
	[07080 'RESPONDS TO SUBORDINATE *BECAUSE*]
	print "[line break][tab]I LIKE YOUR REASONING.[line break]".

To respond to an unrecognized question:
	[07110 'RESPONDS TO *?*]
	print "[line break]";
	increment the unrecognized question count;
	if the unrecognized question count is less than 2:
		[07180]
		print "YES, THAT SEEMS OKAY.[line break]";
		print "[line break][tab][prompt C][line break]";
	else if the unrecognized question count is greater than 2:
		[07210]
		print "THIS QUESTION MAY BE BETTER ANSWERED[line break]DURING THE RESEARCH PHASE.  KEEP IT IN MIND.[line break]";
		print "[line break][tab][prompt B][line break]";
	else:
		[07150]
		print "ANOTHER INTERESTING QUESTION.  I'D SAY 'YES'.[line break]";
		print "[line break][tab][prompt A][line break]".

To encourage elaboration:
	[07240 'RESPONDS TO SHORT ANSWERS]
	print "[line break][tab]AHHH, SHORT AND SWEET.  NOW TELL ME[line break][tab]WHY?  IN OTHER WORDS, ELABORATE A LITTLE.[line break][line break]".

To offer a change of subject:
	[07290 'AUTO NARROW/CHANGE LOOP]
	print "[line break][line break]DO YOU WISH TO NARROW OR CHANGE YOUR SUBJECT?[line break](MAYBE REVISE THE WAY IT SOUNDS IN THESE QUESTIONS?)[line break][tab](YES OR NO?)[line break]";
	if the user agrees:
		change the subject;
	otherwise:
		print "[line break][line break][line break][line break]".


Section 8 - Explaining

To explain the question:
	[07470 <<<   CLARIFICATION ARRAY AND EXAMPLE SEQUENCE   >>>]
	print "[line break]";
	if the current question is explained [already]:
		[09990 'SECOND RESPONSE AFTER CLARIFICATION REQUEST]
		print "[line break]THAT'S ABOUT ALL I CAN ADD AT THE MOMENT.  SORRY![line break]";
		print "[line break][tab][prompt B][line break]";
	otherwise:
		print "[the explanation of the current question]";
		now the current question is explained;
		print "[line break][tab][the follow-up of the current question][line break]".

A follow-up prompt is a kind of value. A question has a follow-up prompt. The follow-up prompts are prompt A, prompt B, and prompt C.

To say (X - a follow-up prompt):
	If X is:
		-- prompt A: [09900]
			say "TRY ANSWERING THIS QUESTION NOW.";
		-- prompt B: [09930]
			say "WHAT ARE YOU THINKING NOW, [first name]?";
		-- prompt C: [09960]
			say "YOUR TURN, [first name].".


Section 9 - Quitting

To quit: [10020]
	if the ask count is less than 3:
		print "[line break][line break][tab]WHY, [first name], YOU ARE IN A HURRY TODAY.[line break][line break][tab]YOU WILL NEED TO SPEND MORE TIME THINKING ABOUT[line break][tab][the subject].[line break][line break][tab]SORRY I COULD NOT HELP YOU MORE.  BYE.[line break]";
	else if the ask count is less than 7:
		print "[line break][line break][tab]YOU ARE DEFINITELY A DEEP THINKER, [first name].[line break][line break][tab]YOU WERE ASKED [ask count] QUESTIONS AND FULLY EXPLORED[line break][tab][explore count] OF THEM.[line break][line break][tab]PLEASE COME BACK AGAIN WHEN YOU CAN STAY LONGER.[line break][line break][tab][tab]GOOD-BYE.[line break]";
	else:
		print "[line break][line break][tab]YOU EXPLORED [explore count] QUESTIONS OUT OF THE [ask count] I ASKED.[line break][tab]THAT'S [(explore count divided by the ask count) times 100] PERCENT.[line break][line break][tab]LET ME REMIND YOU THAT YOU ARE STILL IN THE FIRST STAGES[line break][tab]OF THE CREATIVE PROCESS.  THESE IDEAS MUST SIMMER NOW.[line break][line break][tab]ALSO, I HOPE YOU CAN CREATE SOME OF YOUR OWN 'TOPIC'[line break][tab]QUESTIONS.  I WON'T ALWAYS BE AROUND TO HELP!!![line break][line break][tab][tab]HOPE YOUR PAPER IS TERRIFIC![line break][line break][tab][tab]GOOD BYE & GOOD LUCK![line break]";
	end the story finally;
	[Since we are not using Inform's main loop, we must explicitly add:]
	follow the shutdown rules.



Chapter 5 - Aristotle's Topics

[Finally, we have the topics themselves. These are written out as an Inform table. Tables are written in a "tab separated values" form that is a very bad fit for long text.]

Table of Aristotelian Questions
name	difficulty	text	explanation	follow-up
the opposite question	easy	"WHAT IS THE OPPOSITE OF [the subject]?[line break]"	"SOMETIMES A GOOD WAY TO DESCRIBE SOMETHING IS BY TELLING[line break]WHAT IT IS NOT.  THERE MAY OR MAY NOT BE A DIRECT[line break]OPPOSITE OF [the subject], BUT[line break]SEE IF YOU CAN THINK OF ONE.[line break][line break]FOR EXAMPLE, IF I WERE WRITING A PAPER ON SOLAR[line break]ENERGY, AN ANSWER TO THIS QUESTION MIGHT PRODUCE A[line break]LIST OF EARTH'S NATURAL ENERGY RESOURCES.[line break]"	prompt A
the good consequences question	easy	"WHAT ARE THE GOOD CONSEQUENCES OF[line break][the subject]?[line break]"	"WHAT GOOD WILL COME ABOUT FROM MANKIND'S CONCERN ABOUT[line break][the subject]?[line break][line break]FOR EXAMPLE, IF I WERE WRITING A PAPER ABOUT COLLEGE[line break]ACADEMICS, SOME OF THE GOOD CONSEQUENCES MAY BE A BETTER[line break]JOB IN THE FUTURE, A FULLER UNDERSTANDING[line break]ABOUT OUR WORLD, AND AN APPRECIATION FOR GOOD STUDY HABITS.[line break](STOP THE SNICKERING AND GET ON WITH AN ANSWER.)[line break]"	prompt C
the effects question	easy	"WHAT COULD BE CONSIDERED A RESULT[line break]OF [the subject]?[line break]"	"THIS QUESTION IS ABOUT CAUSES AND EFFECTS, BUT YOUR ANSWER[line break]SHOULD JUST MENTION THE EFFECTS, THE RESULTS, THE[line break]OUTCOMES OF [the subject].[line break][line break]FOR EXAMPLE, IF I WERE WRITING A PAPER ABOUT EXERCISE.[line break]I WOULD WRITE ABOUT A STRONGER HEART, A NEWFOUND[line break]ALERTNESS, AND ANOTHER WAY TO SPEND MONEY (JOGGING SHOES,[line break]TENNIS RACKETS, BICYCLES, WEIGHTS, ETC.)[line break]"	prompt C
the time question	easy	"HOW DOES TIME AFFECT [the subject]?[line break]"	"ARISTOTLE THOUGHT ABOUT TIME AND CHANGE OFTEN.  DOES[line break][the subject] CHANGE OVER TIME?[line break][line break]FOR EXAMPLE, IF I WERE WRITING A PAPER ABOUT DIAMOND MINING,[line break]I MIGHT WANT TO RESEARCH HOW TECHNOLOGY HAS CHANGED THE[line break]MINING PROCESS.[line break]"	prompt A
the inspiration question	easy	"WHAT SPECIAL EXPERIENCES MADE YOU SELECT[line break][the subject] AS YOUR TOPIC?[line break]"	"IF YOU HAVE A GOOD ANSWER HERE, YOU WILL PROBABLY WRITE[line break]A DECENT PAPER.  BY 'SPECIAL', I MEAN 'UNIQUE',[line break]'INTERESTING', OR 'IMPORTANT'.  THESE EXPERIENCES DO NOT[line break]NECESSARILY HAVE TO BE YOURS; YOU COULD PRETEND TO BE A[line break]REPORTER.[line break]"	prompt B
the definition question	easy	"DEFINE [the subject].[line break]"	"YOU MIGHT SPEND ALL DAY ON THIS QUESTION, BUT I AM[line break]AFTER A SHORT DEFINITION.  IN LESS THAN TWENTY WORDS,[line break]WHAT IS [the subject]?[line break]"	prompt C
the causes question	easy	"WHAT COULD BE CONSIDERED A CAUSE[line break]OF [the subject]?[line break]"	"THIS QUESTION IS ABOUT CAUSES AND EFFECTS, BUT YOUR ANSWER[line break]SHOULD JUST MENTION THE CAUSES, THE REASONS,[line break]THE 'WHYS' REGARDING [the subject].[line break][line break]FOR EXAMPLE, IF I WERE WRITING ABOUT HUMAN RIGHTS PROGRAMS,[line break]I WOULD WRITE SOMETHING ABOUT THE[line break]OUTRAGES OF RACISM OUR WORLD WAS WITNESSED.[line break]"	prompt A
the associated objects question	easy	"WHAT OBJECTS DO YOU ASSOCIATE[line break]WITH [the subject]?  HOW MIGHT THEY[line break]BE INCLUDED IN YOUR THEME?[line break]"	"IF I SAY 'BLACK', YOU SAY 'WHITE'.[line break]IF I SAY 'HEADACHE', YOU SAY 'ASPIRIN'.[line break][line break]NOW, [first name], IF I SAY [the subject],[line break]WHAT DO YOU SAY?[line break]"	prompt B
the hypocrisy question	easy	"DOES PUBLIC OPINION ABOUT [the subject][line break]DIFFER FROM PRIVATE OPINION?[line break]"	"BY 'PUBLIC OPINION', I MEAN THE POPULAR POINT OF VIEW.[line break]BY 'PRIVATE OPINION', I MEAN THE WAY PEOPLE ACTUALLY BEHAVE.[line break]SOMETIMES, SUCH IRONIC DIFFERENCES HIGHLIGHT THE OLD ADAGE:[line break]'DO WHAT I SAY, NOT WHAT I DO!'[line break][line break]FOR EXAMPLE, MANY FREE AND LIBERAL THINKERS MAY BE MORE[line break]CONSERVATIVE IN MAKING POLITICAL DECISIONS.[line break]"	prompt C
the what's decided question	easy	"WHAT HAS BEEN DECIDED ABOUT [the subject][line break]TO DATE.[line break]"	"DECISIONS HAVE BEEN MADE ABOUT [the subject].[line break]WHAT WERE THEY ABOUT?  WHO MADE THEM?[line break][line break]FOR EXAMPLE, IF I WERE WRITING A PAPER ABOUT INFLATION,[line break]I WOULD WANT TO WRITE A PARAGRAPH OR TWO ABOUT THE[line break]GOVERNMENT'S LEGISLATION TO DATE.[line break]"	prompt A
the what's undecided question	hard	"WHAT STILL MUST BE DECIDED ABOUT[line break][the subject]? DESCRIBE.[line break]"	"WHAT DECISIONS WILL HAVE TO BE MADE IN THE FUTURE[line break]CONCERNING [the subject].[line break][line break]FILL IN THE BLANKS:  CONCERNING [the subject],[line break]WE MUST DECIDE WHETHER OR NOT TO DO _________________________.[line break]"	prompt B
the connotations-denotations question	hard	"TAKE EACH WORD OF [the subject] INDIVIDUALLY.[line break]WHAT DOES IT MEAN?  CONNOTATIONS?  DENOTATIONS?[line break]"	"A 'CONNOTATION' IS AN ASSOCIATION; A 'DETONATION' IS[line break]A DICTIONARY MEANING.  THIS TACTIC OF THINKING ABOUT[line break]THE INDIVIDUAL WORDS IN A TOPIC OFTEN BRINGS[line break]A FRESSH INSIGHT.[line break]"	prompt B
the bad consequences question	hard	"WHAT ARE THE BAD CONSEQUENCES OF[line break][the subject]?[line break]"	"WHAT BAD WILL COME ABOUT FROM MANKIND'S CONCERN ABOUT[line break][the subject]?[line break][line break]IN OTHER WORDS, WHAT WAS, IS, AND WILL BE THE 'BAD NEWS'[line break]OF THIS TOPIC.  IF YOU CANNOT THINK OF ANYTHING BAD, THEN[line break]WHY NOT?[line break]"	prompt A
the contrarian question	hard	"WHO MIGHT BELIEVE THAT THE GOOD CONSEQUENCES OF[line break][the subject] ARE BAD?[line break]"	"HERE, [first name], WE ARE SEARCHING FOR THE PEOPLE WHO[line break]HAVE COUNTER-ARGUMENTS.  LAWYERS ARE ALWAYS INTERESTED[line break]IN THIS PARTICULAR QUESTION.  MOST ISSUES WE WRITE ABOUT[line break]ARE NOT THAT CLEAR-CUT, NOT THAT 'BLACK AND WHITE.'[line break]"	prompt B
the expert question	hard	"WHO WOULD YOU CONSIDER AN AUTHORITY[line break]ON [the subject]?[line break]"	"BY 'AUTHORITY', I MEAN A SO-CALLED EXPERT.[line break]AS YOU WRITE THE PAPER, YOU MAY QUOTE THESE PEOPLE.[line break]GENERALLY, THEIR OPINIONS ARE RESPECTED--IF NOT BELIEVED.[line break]"	prompt C
the giving question	hard	"WHO GIVES (AND WHO RECEIVES) [the subject]?[line break]"	"I AM OFTEN SURPRISED BY THE CREATIVE ANSWERS TO THIS[line break]QUESTION.  THERE IS USUALLY AN INSIGHT IN UNDERSTANDING[line break]THESE ROLES.  BY 'GIVES', I MEAN 'IS RESPONSIBLE FOR'.[line break]BY 'RECEIVES', I MEAN 'ACCEPTING THE CONSSEQUENCES OF'.[line break]"	prompt C
the authority question	hard	"WHAT MAKES YOU SOMETHING OF AN AUTHORITY ON [the subject]?[line break]"	"YOU PROBABLY DON'T THINK OF YOURSELF AS AN AUTHORITY.[line break]SO PRETEND THAT YOU ARE.  WHAT CREDENTIALS DO YOU THINK AN[line break]AUTHORITY ON [the subject] SHOULD HAVE?[line break]EDUCATION?  POWER?  WEALTH?  COURAGE?  HUMILITY?[line break]"	prompt A
the parts question	hard	"WHAT PARTS OF [the subject] SHOULD BE[line break]DISCUSSED SEPARATELY?[line break]"	"BEFORE SOMEONE CAN UNDERSTAND [the subject],[line break]WHAT MATTERS MUST BE UNDERSTOOD BY THEMSELVES.[line break]"	prompt B
the subtopics question	hard	"DIVIDE [the subject] INTO THREE[line break]SUB-TOPICS.[line break]"	"I LIKE ASKING THIS QUESTION BECAUSE IT MAY HELP YOU ORGANIZE[line break]YOUR PAPER.  WHAT ARE THREE OF THE MAJOR PARTS THAT CREATE[line break]THE WHOLE OF [the subject]?[line break][line break]YOU MIGHT WANT TO WRITE SOMETHING HERE ABOUT HOW THESE[line break]PARTS ARE RELATED.[line break]"	prompt C
the does it makes sense question	hard	"DO ALL ASPECTS OF [the subject] MAKE[line break]SENSE TO YOU?  DESCRIBE THOSE THAT DO NOT.[line break]"	"THIS QUESTION IS INTENDED TO FIND OUT WHAT YOU DO NOT[line break]KNOW ABOUT [the subject].[line break][line break]SO, MAKE A LIST OF THOSE THINGS THAT ARE UNCLEAR -- THE[line break]BEST WAY TO NEW INSIGHTS.[line break]"	prompt A
the general feelings question	hard	"HOW DOES THE GENERAL PUBLIC FEEL[line break]ABOUT [the subject]?[line break]"	"WHAT ARE THE MOST POPULAR OPINIONS REGARDING[line break][the subject]?[line break][line break]IF THERE WERE AN ELECTION ABOUT THIS TOPIC SOMEHOW,[line break]HOW WOULD THE VOTERS RESPOND?  PRO?  CON?  WHY?[line break]"	prompt B
the place question	hard	"WHAT IS THE MOST LIKELY PLACE FOR[line break][the subject] TO EXIST?[line break]"	"WHERE SHOULD I GO TO SEE [the subject]?[line break]CAN I GO INSIDE?  CAN I GOT OUTSIDE?  WHY OR WHY NOT?[line break]"	prompt C
the implication question	hard	"FILL IN THE BLANK:  IF [the subject],[line break]THEN ______________________________________.[line break]"	"THIS IS A TYPE OF INDUCTION, [first name].  I AM NOT TRYING[line break]TO BE TRICKY.  IN OTHER WORDS, IF YOUR TOPIC EXISTS,[line break]THEN OTHER THINGS--FEELINGS, ACTIONS, ETC.--ALSO EXISTS.[line break]TRY MAKING A CONNECTION OR TWO.[line break]"	prompt A
the uniformity of effects question	hard	"ARE THE RESULTS OF [the subject] USUALLY[line break]THE SAME?  DESCRIBE.[line break]"	"BY 'RESULTS', I MEAN THE 'EFFECTS',  YOU MAY HAVE TO DIG[line break]UP A LITTLE HISTORY TO ANSWER THIS QUESTION, OR YOU MAY[line break]HAVE TO PREDICT THE FUTURE.  IN OTHER WORDS, CAN THE[line break]FINAL OUTCOMES OF THIS TOPIC BE PREDICTED OVER AND OVER[line break]AGAIN?[line break]"	prompt B
the general motivations question	hard	"WHAT MOTIVATES PEOPLE TOWARD OR[line break]AGAINST [the subject]?[line break]"	"SIMPLY, WHAT MAKES PEOPLE FEEL THE WAY THEY DO?[line break]MORAL COMMITMENT?  PLEASURE?  FEAR?  PEER PRESSURE?  ETC.[line break]"	prompt C
the persuasion question	hard	"WHAT WILL MAKE PEOPLE CHANGE THEIR MINDS ABOUT[line break][the subject]?[line break]"	"WHAT WOULD IT TAKE FOR MOST PEOPLE TO CHANGE THEIR MINDS[line break]ABOUT [the subject]?[line break][line break]MOST OF THE ANSWERS TO THIS QUESTION HAVE SOMETHING TO DO[line break]WITH A PERSON'S DIRECT INVOLVEMENT WITH A SUBJECT LIKE[line break]YOURS, [the subject].[line break]"	prompt A
the uniformity of causes question	hard	"ARE THE CAUSES OF [the subject] ALWAYS[line break]THE SAME?  DESCRIBE.[line break]"	"ARE THE ROOTS OF [the subject], FIGURATIVELY[line break]SPEAKING, ALWAYS THE SAME?  LOOKING AT THIS MATTER[line break]ANOTHER WAY:  COULD YOU DESCRIBE DIFFERENT EARLY[line break]SYMPTOMS?  OR IS THERE JUST ONE SYMPTOM?[line break]"	prompt B
the incredible question	hard	"WHAT'S INCREDIBLE ABOUT [the subject]?[line break]"	"BY 'INCREDIBLE', I MEAN 'UNBELIEVABLE', 'AMAZING',[line break]'BEYOND HUMAN UNDERSTANDING', 'STRANGER THAN FICTION'.[line break]"	prompt C
the nonuniformity of causes question	hard	"ARE THE CAUSES OF [the subject] ALWAYS[line break]DIFFERENT?  EXPLAIN.[line break]"	"WHAT ARE SOME OF THE DIFFERENT EXPLANATIONS FOR THE[line break]EXISTENCE OF [the subject]?[line break][line break]IF THERE ARE NONE, WHY?  IS THERE[line break]REALLY THAT MUCH AGREEMENT?[line break]"	prompt A
the internal contradictions question	hard	"WHAT CONTRADICTIONS EXIST IN [the subject]?[line break]"	"BY 'CONTRADICTIONS', I MEAN 'THOSE MATTERS WHICH DO NOT[line break]BELONG TOGETHER' OR 'KINDS OF IRONY'.[line break][line break]IN OTHER WORDS, WHAT SHOULDN'T BE THERE, BUT IS?[line break]OR (YOU GUESSSED IT), WHAT SHOULD BE A PART OF[line break][the subject], BUT IS NOT.[line break]"	prompt B
the known unknowns question	hard	"WHAT FACTS ARE YOU UNLIKELY TO KNOW[line break]ABOUT [the subject]?[line break]"	"I BET YOU ARE SAYING TO YOURSELF, 'HOW SHOULD I KNOW?'[line break][line break]WELL, IF YOU ARE GOING TO WRITE A CONVINCING PAPER ABOUT[line break][the subject], YOU MUST[line break]FIND OUT AS EARLY AS POSSIBLE THOSE AREAS WHICH NEED TO[line break]BE RESEARCHED.  RIGHT NOW, I'M ASKING YOU TO PREDICT[line break]WHERE YOU CAN FIND SOME MORE FACTS.[line break]"	prompt C
the clarity question	hard	"ARE ALL THE FACTS ABOUT [the subject] AS[line break]CLEAR AS YOU WOULD LIKE?  DESCRIBE THE AMBIGUITIES.[line break]"	"WHAT PROBLEMS DO YOU HAVE UNDERSTANDING[line break][the subject] YOURSELF?  BY 'AMBIGUITIES', I[line break]MEAN THOSE MIXED FEELINGS YOU MAY HAVE ABOUT THIS TOPIC.[line break]"	prompt A
the better course question	hard	"WHAT IS A 'BETTER COURSE' FOR[line break][the subject] TO TAKE?  RECOMMENDATIONS?[line break]"	"BY 'BETTER COURSE', I MEAN FOR YOU TO SUGGEST A BETTER[line break]SOLUTION TO ANY PROBLEMS ASSOCIATED WITH[line break][the subject].[line break][line break]IF YOU EXPECT PEOPLE TO BE CONVINCED BY YOUR ARGUMENT,[line break]YOU MUST OFFER THEM A SOUND SOLUTION.[line break]"	prompt B
the worst thing question	hard	"WHAT WOULD BE THE WORST THING THAT COULD HAPPEN TO[line break][the subject]?[line break]"	"IF PEOPLE WERE NO LONGER CONCERNED ABOUT[line break][the subject], WOULD THAT BE[line break]THE WORST THING THAT COULD HAPPEN?  WHY OR WHY NOT?[line break]"	prompt C
the best thing question	hard	"WHAT WOULD BE THE BEST THING THAT COULD HAPPEN TO[line break][the subject]?[line break]"	"IF EVERYONE IN THE WORLD WAS AS CONCERNED ABOUT[line break][the subject] AS YOU ARE,[line break]WOULD THAT BE THE BEST THING THAT COULD HAPPEN?[line break]WHY OR WHY NOT?[line break]"	prompt A
the previous mistakes question	hard	"WHAT ARE SOME OF THE PREVIOUS MISTAKES ABOUT[line break][the subject]?[line break]"	"SIMPLY, WHAT HAS BEEN WRONG WITH THE WAY[line break][the subject] HAS BEEN HANDLED.[line break]MAYBE 'MISTAKE' IS TOO HARSH A TERM; 'MISTREATMENT' MAY[line break]BE BETTER FOR THIS TOPIC.[line break]"	prompt A
the complex induction question	hard	"FILL IN THE BLANK:  IF [the subject][line break]PLUS ______________, THEN ______________.[line break]"	"THIS QUESTION ASKS YOU TO CREATE A COMPLICATED[line break]INDUCTION.  THINK OF IT IN MATHEMATICAL TERMS:[line break][line break][tab]IF 2 + ? THEN ?[line break][line break]THERE ARE MANY ANSWERS (2+2=4, 2+90=92,....).[line break]"	prompt B
the what's inconsistent question	hard	"WHAT'S INCONSISTENT ABOUT [the subject]?[line break]PLACES?  PEOPLE?  ACTIONS?  PURPOSES?[line break]"	"BY 'INCONSISTENT', I MEAN TO SUGGEST THOSE MATTERS[line break]WHICH SEEM 'OUT OF PLACE.'[line break][line break]'INCONSISTENT' MAY ALSO SUGGEST THAT SOME THINGS ABOUT[line break][the subject] CHANGE MORE OFTEN[line break]THAN OTHER THINGS.  WHAT MIGHT THEY BE?[line break]"	prompt C
