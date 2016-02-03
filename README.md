<h1>Writing your own kata – a step by step guide</h1>
<p>Writing codewars kata is hard. You’re producing something that you’re hoping will be fun and challenging for a community that while supportive, has high expectations for your work. This guide is a roadmap for beginners who want to write their own kata. It’s more my opinion than an iron-clad guide and it draws on personal experience and existing documentation to provide a suggested route for coming up with good kata. Soon your discussion section will be filled with “Nice kata mate!” and not “Needs random tests + description unclear”. The language used throughout the guide is Javascript.</p>
<h2>Step 1 – Come up with an idea</h2>
<p>According to Wikipedia, “Kata (型 or 形 literally: "form"), a Japanese word, are the detailed choreographed patterns of movements practised in many traditional Japanese arts, most commonly known for their presence in the martial arts, such as aikido, judo, kendo and karate.”</p>
<p>Much in the same way that a martial arts kata requires a series of moves to be carried out in a controlled environment in order to hone one’s body and mind for combat, so codewars kata can be seen as exercises to help programmers improve their skills and knowledge of the language they are working in. You should approach writing a kata with this frame of mind. Which language feature am I testing knowledge of? What skills will be required?</p>
<p>If you’re short of inspiration, a good place to start is to think of a something you learned recently, such as sorting an array or regular expressions, then to try to use that to solve a real life problem you might have had. Think about what you’re testing and what level warrior the kata might be suitable for but don’t forget if you want the warrior to come away feeling like they’ve learned something to follow golden rule #1!</p>
<h5>Golden rule 1 – Give it a twist!</h5>
<p>Martial arts kata are executed as a series of steps, turns, kicks, punches and sword slashes. So must your kata require the user to carry out a series of mental turns and calculation steps. There are other places on the web to practice syntax :p In more advanced kata, the twist is often the requirement for optimisation through a time limit. At a beginner level it might take the form of:<p>
<ul>
<li>Fulfilling multiple requirements from the same method e.g. instead of removing all the spaces from a string with a regex, reducing any instances of multiple spaces to just one space with a regex.</li>
<li>Additional computation e.g. instead of returning an array of numbers in a range, returning an array of all the prime numbers in a range.</li>
<li>Formatting requirements e.g. instead of returning an array, returning an array sorted in a particular way.</li>
</ul>
Still stuck for inspiration? Try having a look at other people’s kata. Could you ask the user to do something similar but with a twist? Could you stitch two existing kata together to make something new and interesting? You’re going to have to look through other people’s kata anyway if you follow golden rule #2!
Golden rule 2 – Search for duplicate kata
Don’t worry, you’re not on Stack Overflow so you won’t get actually crucified for posting a duplicate kata, but you may get mildly tarred and feathered. And certainly as the number of kata on the site increases, this rule will become ever more important. But what is and is not a duplicate?
Duplications spring up naturally as authors try to use established concepts to test programming skill, for example sudoku or the Fibonacci sequence. And who can blame them? Imagine having coming up with a new game every time or defining your own sequence of numbers! The problem arises when the solution for one kata can be pretty much copy-pasted into another one, or lifted straight from a well-known textbook. Not much of a challenge anymore! This is why the community will rinse you out if you haven’t followed the second golden rule and at least added your own twist or angle to existing kata.
Step 2 – Draft description and name
So you’ve finally got an idea you want to run with. Well done you, that’s half the battle! I find a good step at this stage is to open up the new kata tab [screenshot] and to give your kata a provisional name and draft description. This has two benefits:
•	You can refer back to this draft description as you are writing the rest of the kata so it’s useful as an aide-memoir both for that and generally should you decide to go and work on something else.
•	Writing the kata requirements focusses you mind on what the kata will actually look like and can help guide the tests you are about to write. E.g. Do I want the user to return a number or a boolean? What would a good name the function be?
At this stage it can be a summary of what the user will be asked to do. You can refine it as you go along and finalise before you publish.
Step 3 – Write basic tests
Now you know what you want your user to do it’s time for your first test. Test Driven Development (TDD) involves, among other things, following the practice of writing the test before you’ve written the solution. The full test reference docs can be found here http://www.codewars.com/docs/js-slash-coffeescript-test-reference , but as a general rule you will be using `Test.assertEqual` when a string, number or Boolean is returned and `Test.assertSimilar` when an array or object is returned. I’m going to talk about `Test.assertEquals` here but they work the same way.
`Test.assertEquals` takes three arguments:
Test.assertEquals(the user’s solution, the correct answer, a message if the test fails)
It returns true or false based on whether or not the first two arguments evaluate to the same value. You should choose some inputs then figure out one or two outputs from the kata solution and put them into the second argument. For example if your function `solution` returns a number double the value of the argument it takes then your first test might look like this:
`Test.assertEquals(solution(2), 4, “Should return double the given argument!”)`
Write your first tests into the Test cases box on the bottom right-hand side. Now it hit the green validate solution button. Oh dear it failed! Now all we have to do is write something that passes!
Testing will only be touched upon briefly in this guide. The docs on the Codewars website actually aren’t brilliant for testing but Section 4 of the Conjured Codewars Codex http://bkaestner.github.io/codewars-rules/ covers testing in more detail.
Step 4 – Write your solution
Now like you’ve been doing so far on codewars, write a function that fulfils the requirements of the test. Things are likely to change at this stage because you’ve realised that what is in the description is too easy or too hard or just not interesting. Make sure you keep the draft description updated if you do change anything.
Step 5 – Test for edge cases
A good set of tests should work together as a team. Imagine each test as an obstacle on an assault course. https://upload.wikimedia.org/wikipedia/commons/6/63/Clyne_Farm's_assault_course_-_geograph.org.uk_-_791094.jpg 
Only a solution that can climb over every wall, crawl through every tunnel and swim through every stream should get through to the other side. If you write tests that only ask the solution to climb over walls then how do you know that it has met the required specification? That’s why it’s important to follow golden rule #3.
Golden rule 3 – Test for edge cases
An edge case test can probably best be described as a test that if the user has missed part of the description, will trip them up. At its most basic, it will test of implementation of the expected control flow. For example, I want a function that doubles its given argument unless the argument is an odd number, in which case I want it to triple its given argument. I would make sure that at least one of the tests covers this case:
`Test.assertEquals(solution(1), 3, “Should return triple the given argument!”)`
I would make sure that each element of the description is covered in this way. You can also use this method of testing functionality piece by piece to write your own solution.
You should write each test case so that it ‘only just’ passes. An example for a kata that mentions 10 minutes in its description is a test that will fail you if you forget that 10 minutes is 0.1666 of an hour NOT 0.1 of an hour. Look for opportunities to pick out the edges like this and once you’ve got the major bases covered then you’re ready to follow golden rule #4.
Golden rule 4 – Example tests
The general convention is that if a solution passes the example tests it should stand a good chance of passing the full testing suite. It might get picked off by the random tests or require a rethink because it runs too slowly and the full tests require optimisation but with your random tests you should be giving your users a very clear indication of what you’re looking for. Some kata have no example tests. Some kata have very few examples, then the full testing suit has totally unexpected demands. Don’t do this. It’s annoying. Write carefully edged example tests with helpful error messages that enable the user to build their function piece by piece.
Step 6 – Random tests
•	What are random test and why are they important?
Golden rule 5 – Random tests
Step 7 – Final description
•	Reformat and check in preview box to make sure markup is coming through correctly.
•	Go away and do something else then come back to re-read your description.
•	Remember many people on the site have English as their first language.
Golden rule 6 – Double-check your description
Step 8 – Estimated rank and tags 
•	Go to the kata page to see what tags fit your kata
Step 9 – Publish!
Golden rules checklist
•	Post in the gitter
•	Use in the JS folder
Step 10 – Stay involved
•	Duty of stewardship. Especially in the first 24/48 hours. Where to find notifications.
•	Check and approve translations
•	Get a super user to approve.
•	Check the authored kata tab
•	Check the discourse needs resolution tab
