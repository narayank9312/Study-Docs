Here is the complete content of the "Soni Frontend Sheet" formatted for Obsidian:

---

# Soni Frontend Sheet

Hey There👋  
Hope you are Doing Well!

In this document I have covered:
- Things to keep in mind while going for each topic
- My Interview Experience on each topic
- Video/articles/Resources are attached with each topic

Let's get started with Interview Preparation, All the Best!

## Generally, I have seen there are 4-5 rounds for most of the Product based companies:
1. JavaScript
2. Machine Coding / React
3. DSA
4. System Design
5. Managerial Round

### JavaScript
1. Common Questions - These are some common conceptual questions asked during the first phase of the interview to understand your fundamentals and core concepts.

   a. Lexical Scoping  
   b. Hoisting, Temporal Dead Zone  
   c. Closure  
   d. ES6 feature (let var and const, template literal, Destructuring, promises, class module etc)  
   e. Is JavaScript Asynchronous Language?  
   f. Events in JS? Event bubbling and capturing?  
   g. Difference between web worker and service worker.  
   h. Write a Memoization function?  
   i. ‘this’ in JS  
   j. Prototype and Prototypal inheritance  
   k. How Browsers work when you hit on a URL?  
   l. Local Storage vs Session Storage vs Cookies?  
   m. Web APIs like setTimeout & setInterval  
   n. Infinite Scroll  

   Resources:  
   - [What happens when you type an URL in the browser and press enter](https://medium.com/@maneesa/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a)  
   - [Video](https://youtu.be/MOd5cTJ6kaA)  

2. Polyfills/ Implementation-based Questions  
   a. Promise.all(), Promise.any()  
   b. Clear all timeouts  
   c. Flat array Array.flat() in both recursive and iterative ways.  
   d. Flatten Object  
   e. Pipe and compose  
   f. Higher Order Functions like Map, Reduce, Filter, Sort  
   g. Call, apply, bind  
   h. [ShareChat, Easy] - Print numbers 1 to 10 in a time interval of 1 sec and update on UI.  
   i. [Publicis sapient, Easy] - Debouncing and Throttling Solution  
   j. [Tekion, Easy] polyfill which gives us the count of vowels in a string.  
   k. [Tekion, Medium] - Implement virtualization table in JS.  
   l. [Pubmatic, Medium] Method Chaining Solution  
   m. [Tekion, Hard] Implement Promise class with handling of error bubbling upstream.  
   n. [Swiggy, Medium] - polyfill for JSON.stringify Solution  
   o. [Meesho, Medium] - Implement Lodash polyfill groupBy  

   Questions  
   - What if arguments are functions?  
   - What if arguments are a mixture of function, string, number, and promise?  
   - How will you handle async call in groupBy Solution?

   Code snippet - If you are good with the above parts like (this in JS, hoisting, temporal dead zone, execution flow in JS) you can easily answer the code snippet part but read the question carefully and ask for hints if you feel stuck. Best way to practice these questions is either by dubbing or discussing. You can read others' interview experiences from LeetCode and get some questions from it.  

   Resources:  
   - [Lydia Hallie](https://github.com/lydiahallie/javascript-questions)  
   - [Sudheerj JS](https://github.com/sudheerj/javascript-interview-questions)  
   - [Video](https://youtu.be/Zo-6_qx8uxg)  
   - [Method Chaining in JavaScript](https://dev.to/isiakaabd/method-chaining-in-javascript-154a)  
   - [Video](https://youtu.be/VGvvyS4qTsw)  
   - [Lodash groupBy](https://lodash.com/docs/#groupBy)  
   - [LeetCode Interview Experience](https://leetcode.com/discuss/interview-question?currentPage=1&orderBy=hot&query=)  

   Resources:  
   - [Namaste JavaScript](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP) (Best one to start)  
   - [Learns Bucket](https://learnersbucket.com/)  
   - [FrontEnd Master](https://frontendmasters.com/courses/javascript-hard-parts-v2/)  
   - [Big Frontend](https://bigfrontend.dev/)  

### HTML/CSS (Frequently asked questions)
1. Difference between (display: none, visibility: hidden, opacity: 0)  
2. What are ways to hide elements in DOM.  
3. Pseudo class/ pseudo selector.  
4. What is a box model?  
5. Semantic element vs non-semantic element.  
6. Focus on layouts, positioning, responsive design techniques, CSS preprocessors (e.g., Sass, Less), and any frameworks like Bootstrap or Material-UI.  
7. Web accessibility  
8. SEO  
9. How rendering works (Reflow vs Repaint)  
10. Centering of div  
11. Async and defer  

   Resources:  
   - [W3 Schools](https://www.w3schools.com/)  
   - [CSS](https://learnersbucket.com/)  
   - [Code with Harry (With Basics)](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP)  
   - [Best way to Learn HTML/CSS using Build 2-3 web projects](https://www.youtube.com/playlist?list=PLZlA0Gpn_vH9D0J0Mtp6lIiD_8046k3si), you can start with your portfolio  
   - [How browsers work](https://www.youtube.com/watch?v=BsDoLVMnmZs&t=7162s)  

### Machine Coding Questions
Whether you are a junior or senior developer, they will give you a small module to build from scratch either on React or on JS.

Things to keep in mind while doing Machine Coding round:
1. Understand requirements clearly, ask doubts if any then and there.  
2. Take some time to think about the complete flow and folder structure.  
3. Focus majorly on the logic part, don't waste your time on CSS and HTML first, complete the minimum basic requirement.  
4. Make it interactive as much as you can.  
5. Freshers can include clones for YouTube, Netflix, Medium.  

   Resources:
   - [Understand the requirements fully and prepare a rough sketch in your mind](https://www.google.com/search?rlz=1C5GCEM_enIN1006IN1006&sxsrf=AB5stBiKH3RFItSsI9jco9T5BTqBbMAc0g:1689503407946&q=understand+the+requirements+fully+and+prepare+rough+sketch+in+your+mind+with&spell=1&sa=X&ved=2ahUKEwiMvOjTgpOAAxUfS2wGHZqeBagQBSgAegQICRAB)  

1. Common Questions
   - Design popover on click of any product  
   - Design Accordion  
   - Movie application  
   - Star Rating  
   - [Commonly asked] Listing product details (infinite scroll), searching, sorting, pagination  
   - [Amazon Assessment] Design Carousel  
   - [Google domain specific round] Nested checkbox / Nested comment box  
   - [Commonly asked] Flash card  

2. [ShareChat, Medium]
   - Build login form and store data in local storage.  
   - Build a signup form and if the user exists, go to the HOME page else show an error on the UI.  

3. [CRED] - Build feature Google search + Auto suggestions  
   - How can you make the search more performant?  

4. [Amazon, Medium] - File management system  
   - Directory might contain files with different extensions (xml, pdf, json and size) or nested directories till n level of hierarchy.  
   - Design interface how it looks like then follow up questions asked:  
     i. Find all files having xml extension  
     ii. Find all files having sizes greater than 5mb  
     iii. If I want a file having an xml extension and size greater than 5 mb, how will you make your function reusable?  

5. [Amazon, Medium] - Display all products on UI (data coming from API) which can be filtered based on tags (rendered as checkbox)  
   - On click on any image model should display image title and image and date in MM/DD/YY format.  
   - Display all tags in the form of checkboxes and if I check multiple tags, then images should be filtered on that basis.  
   - Handle event delegation (on each image or on the parent container).  

6. [Media.net, Medium] Shopping Cart Application  

7. [Uber, Hard] - Build a calculator using HTML, CSS, and JS with basic functionality like addition, subtraction, multiplication, division, bracket, equal button. Build

 an eval function on top of it.  

8. [Atlassian, Medium, Commonly Asked] - Build Page tree/ Nested folder  

   Resources:  
   - [Namaste React](https://namastedev.com/namaste-react/)  
   - [Dev Tool](https://www.youtube.com/devtoolstech/videos)  
   - [RoadSide coder](https://www.youtube.com/playlist?list=PLKhlp2qtUcSYQojD5G-ElgHezoCyq2Hgo)  
   - [Learners bucket](https://www.youtube.com/results?search_query=learners+bucket)  
   - [Sudheerj React](https://github.com/sudheerj/reactjs-interview-questions)  
   - [JS Cafe](https://www.youtube.com/@js_cafe)  
   - [Sadanand Pai Git](https://github.com/sadanandpai/frontend-learning-kit)  

### DSA Strategy
If you are trying for reputed product-based companies, then don’t ignore DSA, it is a game-changer.

1. Focus majorly on Array, String, linked list, Sliding window, two pointer, Recursion and tree.  
2. You can practice for daily 3 questions in which two of them should be of Array and String and the third one you can choose from other topics with initially EASY and MEDIUM level only and be consistent on this part. Don't directly jump for hard questions, else you will feel frustrated and lose confidence at the initial stage itself.  
3. Focus majorly on questions that are highly Voted and liked on Leetcode as the probability of those questions in the interview is very high.  
4. As a FE Engineer, you will be asked to solve problems in the JAVASCRIPT language. Practice DSA in JS Only.  

   Resources:  
   - [Namaste React](https://namastedev.com/namaste-react/)  
   - [Dev Tool](https://www.youtube.com/devtoolstech/videos)  
   - [RoadSide coder](https://www.youtube.com/playlist?list=PLKhlp2qtUcSYQojD5G-ElgHezoCyq2Hgo)  
   - [Learners bucket](https://www.youtube.com/results?search_query=learners+bucket)  
   - [Sudheerj React](https://github.com/sudheerj/reactjs-interview-questions)  
   - [JS Cafe](https://www.youtube.com/@js_cafe)  
   - [Sadanand Pai Git](https://github.com/sadanandpai/frontend-learning-kit)  

5. During the interview, take a moment to understand the problem completely and start with brute force to an optimized level. If you get stuck, ask for hints without hesitation.  
6. Again I recommend go and read others' interview experiences on Leetcode, you will find a pattern that there are some questions that are very frequently asked for the initial level like:
   - Remove duplicate elements from an array.  
   - Sorting of an array.  
   - 3 Sum problem  
   - Find the first and second and third maximum elements in an array.  

   Resources:  
   - [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)  
   - [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)  
   - [3 Sum](https://leetcode.com/problems/3sum/)  
   - [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)  
   - [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)  
   - [Number of Matching Subsequences](https://leetcode.com/problems/number-of-matching-subsequences/)  

### System Design Guidelines
Here are some of the things you should think about before jumping into the solution:
1. Gather the requirements and ask for edge cases if any.  
2. Write function and non-functional requirements.  
3. Be interactive during the whole session.  
4. Important topics to touch while designing the solution:
   - CDN  
   - Performance  
   - Deployment  
   - Analytics Monitoring/Logs  
   - PWA  
   - Data Recovery  
   - Accessibility  
   - Cross-browser compatibility  
   - Single Point of Failure  
   - Scalable  
   - Security  
   - Micro-frontends  
   - Database/Design APIs/Storage - S3, EC2, EBS  
   - SEO  
   - State management  

5. [Amazon, Medium level] - Design a newspaper application
   - Requirements  
   - Design Component structure  
   - User authentication and authorization  
   - Sharing news with other people  
   - How will you make sure it is accessible to most people  
   - Performance-related issue  
   - If there is any hot news about how client-side interacts with server-side.  
   - How will you show related articles to hot news?  
   - How data will flow from frontend to backend and asked to create the interface of each API.  

6. [Appsmith, Medium] Build functionality for an application like Twitter
   - How can I add or remove users?  
   - If a user posts anything, to whom it should be visible and follow up, what if I blocked some users.  
   - How will we handle if a particular post is reported as spam by so many users?  
   - How can I suggest mutual friends to a user?  
   - Nested component or chat, etc.  

   Resources:  
   - [Chakde System Design](https://www.youtube.com/playlist?list=PL4CFloQ4GGWICE0Tz6iXKfN3XWkXRlboU)  
   - [JS Cafe](https://www.youtube.com/@jsconf_/videos)  
   - [FrontEnd Engineer](https://www.youtube.com/@FrontEndEngineer)  

### Managerial Round
This round is generally for team fit or behavioral round.

1. This round will be more on project discussion and situation-based questions like:
   - What do you do when you get critical feedback from a client/manager?  
   - What was the biggest tech problem you have faced and how did you approach that problem?  
   - Share an instance when you took ownership of any project or module?  

2. Tech-related questions
   - Browser related questions  
   - Project discussion  
   - Optimization and performance  
   - Your previous role and contribution  
   - JS and framework related stuff  

### Resume
Old Resume: [Here](https://drive.google.com/file/d/1l6GpyfIT5vxrKaQNP2LLiLYKkYXPIeqY/view?usp=sharing)

1. Keep your resume simple and straightforward which technically sounds good.  
2. The resume should be one page only, it is easy to read. Don't go for a two-column resume, it is hard for ATS (Initially I made it in 2 columns but later I realized).  
3. Make it ATS friendly like always try to include keywords like Developed, Exceeded expectation, Delivered Result, performance, Reduced etc and add some data points. For eg:
   - Increased performance from X to Y%.  
   - Reduced Initial time load from 3s to 2s.  
4. Try to use bullet points and avoid colorful templates.  
5. Upload your resume in Google Drive, and share the link.  
6. Highlight/Bold the topics which you want to be eye-catching for the interviewer.  
7. Best resources for one pager resume is overleaf Template 1, Template 2 or you can try JobScan
8. For Freshers - Internship Project/ personal project > Technical skills > Education and achievements  
9. For Experienced - Work experience projects > personal project > Technical skills > Education and achievements  

   Resources:  
   - [Modern Deedy Resume Template](https://www.overleaf.com/latex/templates/modern-deedy/cxtjgrmpsrvh)  
   - [Resume Template by Anubhav](https://www.overleaf.com/latex/templates/resume-template-by-anubhav/dhmkrwtksdgy)  
   - [JobScan](https://www.jobscan.co/)  

### How to approach for Job on LinkedIn and Referral strategies
1. For me three platforms worked very well - LinkedIn (Best one), Naukri.com, instahyre but don't leave other platforms like tophire, cutshort, Hirect.
2. Create a list of your target companies.  
3. Find connections related to each company on LinkedIn around 30-40+ people and send them requests with a personalized note. This will definitely increase the chance of accepting requests.  
4. Build a common referral message and send it to connections during office hours so chances of getting referrals will be instant else they might ignore.  
5. Ask for a referral to as many people as you can as the general ratio of getting responses is 1:10.  
6. Provide a heading Frontend Engineer Referral, Amazon (Job Id) and link to your resume in advance and straightforwardly ask for a referral.  
7. For freshers, you can attach your personal project or portfolio link.  
8. Your initial 4-5 words will play a crucial role, generally, it will decide that the person will find interest in you and get you referred.  
9. If you don't get any reply just send a follow-up for a gentle reminder.  
10. Still no response, go to the career page and apply for companies.  
11. Update your LinkedIn profile professionally, meaning each section like About, Skill, Recommendation etc as it gives more confidence to the person giving you

 a referral.  
12. LinkedIn is your First resume and present it wisely. Try to show your visibility on LinkedIn via posting technical-related stuff so people might recognize your activity. It might happen that the recruiter/manager might reach out to you when they have a demand.  

You are Good to Go for interview preparation🙂

You can connect with me here: [LinkedIn](https://www.linkedin.com/in/shubham-soni-374a86175/)

Thanks,  
Shubham Soni

---