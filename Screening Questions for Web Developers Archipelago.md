![horizontal line]

![short line]

<a name="_kk1966kbedef"></a>Developer
**Screening Questions**

![short line]
# <a name="_vrhvb96nxxe9"></a>Summary
Depending on the job you’re interviewing for, you might not need to be able to answer all of these questions to get an interview.  If you don’t know how to do a section or a question, you can skip it.  However, if you’re interviewing for a senior position you should be able to answer all 3 levels for your role (Senior Backend Devs Must Complete the level 3 database question.  FrontEnd Devs must complete *at least* level 1 and level 2.)
# <a name="_gyxphb3fgeqp"></a>How To Answer
1. Please answer the questions on an md file. We prefer that you host the md file on your own public git repo but you can also just attach the md file on your reply email. 
1. For coding questions, please make sure your code can be executed directly after copy pasted to any online js playground or fiddler and achieve the requested result.
1. For codes that need to be set up locally, please add the guideline on how to set up and execute your code.
# <a name="_7hd6knfpgxbm"></a>
# <a name="_2fcxmmu2nm4o"></a>Basic Questions
Imagine you're building a website that allows users to submit photos. One of the requirements is that each photo must be reviewed by a moderator before it can be published. How would you design the logic for this process? What technologies would you use? Do you have any data structure in mind to support this based on your technology of choice to handle those data? 
### <a name="_w4b27r8937nn"></a>**The High Level Logic & Flow for The Website:**
1. **Photo Submission by User:**
   1. User submits a photo by uploading it.
   1. Photo is saved in a storage service like Google Cloud Storage, AWS S3.
   1. Metadata (photo ID, uploader, timestamp, status, and any other details) is saved in the database.
   1. A notification for the moderator is created to review the photo.
1. **Review by Moderator:**
   1. Moderator views pending photos through a dashboard.
   1. Moderator can APPROVE or REJECT the photo and add a note for the reason for rejection.
   1. On approval: Status is set to APPROVED and the photo becomes publicly visible for the user via Frontend/API.
   1. On rejection: Status is set to REJECTED and the user may receive a notification.
### <a name="_11zvxsg0ea7h"></a>**Technologies**
**Frontend:**

- React (or Next.js) for both the user-facing site and admin dashboard.

**Backend:**

- **Node.js + Express / NestJS** or **Django** (depending on the team preference)
- **REST API**


**Database:**

- **PostgreSQL** for the structured data and relational need

**Storage:**

- AWS S3 / Google Cloud Storage for actual image files.
- The database will only store the path to the image in the storage service.
### <a name="_cxe7ne6if06j"></a>**Data Structure**
interface Photo {

`  `id: string;

`  `userId: string;

`  `url: string;

`  `status: 'PENDING' | 'APPROVED' | 'REJECTED';

`  `createdAt: Date;

`  `reviewedBy?: string; // Moderator ID

`  `reviewedAt?: Date;

`  `rejectionReason?: string;

}


# <a name="_8mxtxaf2l6vp"></a>
# <a name="_fnjk6vnqzbqk"></a>Database Questions (Skip if no experience)
Open this link: [Basic SQL Emulator](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all)

**Level 1 (Novice - Expected Task Time: 1 minute):**

Write a SQL query that shows me how many customers there are from Germany.

SELECT \* FROM Customers where Country = 'Germany';

**Level 2 (Business Admin - Expected Task Time <4 minutes):**

Write a query that shows me a list of the countries that have the most customers; from most customers to least customers.  Don’t show countries that have less than 5 customers.

Answer:

SELECT Count(CustomerID) as 'COUNT(CustomerID)', Country FROM Customers GROUP BY Country having Count(CustomerID) > 4 ORDER BY Count(CustomerID) DESC;

**Level 3 (Average Developer - Expected Task Time <8 minutes):**

Reverse Engineer These Results (tell me the query that we need to write to get these results):

SELECT c.CustomerName, COUNT(o.OrderId) AS 'OrderCount', MIN(DATE\_FORMAT(o.OrderDate, "%Y-%m-%d")) AS 'FirstOrder', MAX(DATE\_FORMAT(o.OrderDate, "%Y-%m-%d")) AS 'LastOrder' FROM Orders o INNER JOIN Customers c on o.CustomerId = c.CustomerId GROUP BY o.CustomerId, c.CustomerName HAVING COUNT(o.OrderId) > 4 ORDER BY MAX(o.OrderDate) DESC;

Actually using the link [Basic SQL Emulator](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all) the query above will return an error, because the version in there, but it’s working well in the correct sql version. The working version is below but has different date format from the requested one:

SELECT c.CustomerName, COUNT(o.OrderId) AS 'OrderCount', MIN(o.OrderDate) AS 'FirstOrder', MAX(o.OrderDate) AS 'LastOrder' FROM Orders o INNER JOIN Customers c on o.CustomerId = c.CustomerId GROUP BY o.CustomerId, c.CustomerName HAVING COUNT(o.OrderId) > 4 ORDER BY MAX(o.OrderDate) DESC;

# <a name="_2fup1svvujrd"></a>
# <a name="_chto247rp9sq"></a>JavaScript/TypeScript Questions
Answer as many levels as you can… the level you reach will only affect the type of position you’re qualified for - we have many positions available.  But if you don’t complete level 1, you won’t get an interview.

**Level 1: Expected Task Time <15 minutes.**

Make a javascript or typescript function that converts any string to Title Case.


Expected Results:

|titleCase("I'm a little tea pot") should return a string.<br>titleCase("I'm a little tea pot") should return "I'm A Little Tea Pot".<br>titleCase("sHoRt AnD sToUt") should return "Short And Stout".<br>titleCase("SHORT AND STOUT") should return "Short And Stout".|
| :- |

Or

**Create a function that counts the word frequency in this string "Four One two two three Three three four  four   four".  Case insensitive, ignore punctuation.**

**Expected Answer:**

**one => 1**

**two => 2**

**three => 3**

**four => 4**

**Code:**

**function freqCount(*s*) {**

` `**let ret = ''**

` `**var wordsCount = {}**

` `**s = s.toLowerCase().replaceAll(/[^0-9a-z]/gi, " ").replaceAll(/\s+/g, " ")**

`  `**s.trim().split(" ").forEach(function(*word*, *\_i*, *\_arr*) {**

`   `**wordsCount[word] = wordsCount[word] ? ++wordsCount[word] : 1;**

` `**})**

` `**for (const [key, value] of Object.entries(wordsCount)) {**

`   `**ret += key + " => " + value + "\n"**     

` `**}**

` `**return ret**

**}**

**s = "Four, One two two three Three three four  four   four"**

**console.log(freqCount(s))**


**Level 2:  Expected Task Time 1 minute.**

Fix this code, using promises:

Answer:

|<p>**function delay(ms) *{<br>`  `// add promise code here<br>`  `return new Promise(resolve => setTimeout(resolve, ms));***</p><p>***}*<br><br>delay(3000).then(() => alert('runs after 3 seconds'));**</p>|
| :- |

**Level 2.5: Rewrite using Async/Await:**

|<p>**function fetchData(*url*, *callback*) {**</p><p>`  `**setTimeout(() => {**</p><p>`    `**if (!url) {**</p><p>`      `**callback("URL is required", null);**</p><p>`    `**} else {**</p><p>`      `**callback(null, `Data from ${url}`);**</p><p>`    `**}**</p><p>`  `**}, 1000);**</p><p>**}**</p><p></p><p>**function processData(*data*, *callback*) {**</p><p>`  `**setTimeout(() => {**</p><p>`    `**if (!data) {**</p><p>`      `**callback("Data is required", null);**</p><p>`    `**} else {**</p><p>`      `**callback(null, data.toUpperCase());**</p><p>`    `**}**</p><p>`  `**}, 1000);**</p><p>**}**</p><p></p><p>***// Using callbacks***</p><p>**fetchData("https://example.com", (*err*, *data*) => {**</p><p>`  `**if (err) {**</p><p>`    `**console.error("Fetch Error:", err);**</p><p>`  `**} else {**</p><p>`    `**processData(data, (*err*, *processedData*) => {**</p><p>`      `**if (err) {**</p><p>`        `**console.error("Process Error:", err);**</p><p>`      `**} else {**</p><p>`        `**console.log("Processed Data:", processedData);**</p><p>`      `**}**</p><p>`    `**});**</p><p>`  `**}**</p><p>**});**</p><p></p>|
| :- |
**Answer:**

**function fetchData(*url*) {**

` `**return new Promise(function (*resolve*, *reject*) {**

`   `**setTimeout(() => {**

`     `**if (!url) {**

`       `**reject("URL is required");**

`     `**} else {**

`       `**resolve(`Data from ${url}`);**

`     `**}**

`   `**}, 1000);**

` `**});**

**}**


**function processData(*data*) {**

` `**return new Promise(function (*resolve*, *reject*) {**

`   `**setTimeout(() => {**

`     `**if (!data) {**

`       `**reject("Data is required");**

`     `**} else {**

`       `**resolve(data.toUpperCase());**

`     `**}**

`   `**}, 1000);**

` `**});**

**}**

***// Using async/await***

**fetchData("https://example.com").then(*data* => {**

`   `**processData(data).then(*processedData* => {**

`       `**console.log("Processed Data:", processedData);**

`     `**}).catch(*err* => {**

`       `**console.error("Process Error:", err);**

`     `**});**

` `**}).catch(*err* => {**

`   `**console.error("Fetch Error:", err);**

` `**})**

**Level 3-4: Expected Task Time Less Than 1 Hour.**

**Create a real-time chat between two windows; using web sockets, vuejs and typescript.**  Bonus if you add some nice, simple animations.

If you have no experience with web sockets, just make two chat windows side-by-side in the different browser window.  Show messages being sent between the two chat screens.  As new messages come in, old messages slide upwards to make room for new messages.

If you’d like to be considered for a **senior role** or **lead role**, please deploy to AWS and send me a link to your working application.

See example below:


Answer:

<https://github.com/convyusboy/vuechatapp> - the setup is there on readme.md
# <a name="_3jclaalmcxcl"></a>
# <a name="_l7ickivxi45f"></a>Vue.js
- Explain Vue.js reactivity and common issues when tracking changes.

  We can't really track the reading and writing of local variables. There's just no mechanism for doing that in Vue.js. We can do this instead, intercept the reading and writing of object properties. There are two ways of intercepting property access in JavaScript: getter / setters and Proxies. 

  The common issues are working with third-party libraries that aren't designed to be compatible with Vue can be difficult, and sometimes, 2 same methods can have different results.

- Describe data flow between components in a Vue.js app

  There can be two types of data flow between components:

1. Parent component to Child Component - We can send data from the parent component to the child component using props.
1. Child component to Parent Component - We can send data by emitting an event from the Child component and listen to it on the other end (Parent component).
- List the most common cause of memory leaks in Vue.js apps and how they can be solved.

  Memory leaks in Vue.js usually arise due to the improper management of components, global event buses, event listeners, and references.

  To fix the Memory Leaks in Vue.js Applications:

1. Ensure that event listeners are added during the mounted lifecycle hook and removed during the beforeDestroy hook of the component.
1. Be careful when creating circular references between components. If they are necessary, make sure to break the circular references when the components are destroyed.
1. Remove components from the global event bus when they are destroyed using appropriate lifecycle hooks.
1. Use the beforeDestroy lifecycle hook to clean up reactive data properties to prevent them from holding references to the destroyed component.
- What have you used for state management

  I haven’t really used state management in my experience

- What’s the difference between pre-rendering and server side rendering?

  There are several differences between pre-rendering and server side rendering. They are the timing of the rendering (pre-rendering on the build process, server side rendering on user request), content updates (pre-rendering content is static, server side rendering is dynamic), and performance (pre-rendering is usually faster to load, and server side may require more server resources)
# <a name="_ps0bqj5xq4yb"></a>
# <a name="_l4rjbqjssovk"></a>Website Security Best Practises
Tell me all the security best practices you can think of - start with the most important ones first.

To maintain strong security, the best practices are strong authentication, regularly updating software, implementing HTTPS, use a Web Application Firewall (WAF), and maintaining regular backups.

1\. Strong Authentication & Access Control:

- Implement Multi-Factor Authentication (MFA) - verify their identity using multiple methods 
- Use Strong, Unique Passwords - Encourage users to use long, complex passwords and avoid reusing them across multiple sites
- Limit User Privileges - only the access they need to perform their tasks, minimizing the potential impact of a compromised account

2\. Software Updates & Security Patches:

- Keep Software Up-to-Date - content management system (CMS), plugins, themes, and other software to patch known vulnerabilities
- Monitor for Security Updates - get security suggestions and install necessary patches.

3\. Secure Communication (HTTPS):

- Use HTTPS Protocol - to encrypt data transmitted between the server and users, protecting sensitive information
- Install an SSL/TLS Certificate - ensures the secure transmission of data

4\. Web Application Firewalls (WAFs):

- Deploy a WAF - filtering out malicious traffic before it reaches our website
- Configure the WAF - block common threats and vulnerabilities

5\. Backups & Disaster Recovery:

- Regularly Backup The Website - for quick restoration in case of any issue
- Store Backups Offsite - to prevent data loss regarding accident

6\. Security Audits & Monitoring:

- Conduct Regular Security Audits - Review Web’s Config Regularly to prevent any vulnerabilities
- Monitor for Suspicious Activity - Implement monitoring tools

7\. Input Validation:

- Validate User Input - Always validate user input to prevent harmful code injection
- Never Trust User Input - Always sanitize user input
# <a name="_hhzo895wsngz"></a>Website Performance Best Practises
Tell me all the performance best practices you can think of - start with the most important ones first.

To optimize website performance, the best practices are optimizing images, minimizing HTTP requests, leveraging browser caching, enabling compression, and choosing a reliable hosting provider.

1\. Optimize Images:

- Reduce Image Size: Compress images without significant quality loss using known tools Choose the Right Format: Use WebP for better compression and quality 
- Use Lazy Loading: Load images only when they are visible in the viewport to improve initial page load.

2\. Minimize HTTP Requests:

- Combine Files: Combine CSS and JavaScript files into fewer files to reduce the number of HTTP requests
- Use CSS Sprites: Combine multiple small images into a single image and use CSS to display specific sections
- Reduce External Scripts: Minimize the use of external scripts and fonts, as they can slow down page loading

3\. Leverage Browser Caching:

- Set Appropriate Cache Headers: Configure the server to cache static assets like images, CSS, and JavaScript
- Use Long Cache Expiration Times: Allow browsers to store assets for longer periods to reduce server load

4\. Enable Compression:

- Use Gzip Compression: Compress text-based assets like HTML, CSS, and JavaScript to reduce file size and improve transfer speed
- Enable Brotli Compression: Consider using Brotli for even better compression, especially on modern browsers

5\. Choose a Reliable Web Hosting Provider:

- Select a Provider with Fast Servers and Good Uptime
- Consider Server Location: geographically close to the target audience
- Choose a hosting plan that suits the needs 

6\. Other Important Considerations:

- Minimize Redirects: Avoid unnecessary redirects, as they can slow down page load times 
- Optimize Fonts: Use web fonts sparingly and optimize their loading
- Use a Content Delivery Network (CDN): Distribute the website content across multiple servers to improve loading speed for users in different locations
- Optimize for Mobile: responsive and loads quickly on mobile devices. 
- Monitor Performance Regularly and Test the website speed: Use tools like Google PageSpeed Insights to identify performance issues, website speed, and improvements
- Load test the website: Use tools like KeyCDN to test the website under heavy load
- Fix 404 errors: Ensure all links on the website are working.
- Serve scaled images: in the correct size for the device they are being viewed on. 
- Database optimization
# <a name="_3f682chiqks3"></a>
# <a name="_xyobv7baaj59"></a>Golang (if interviewing for a Golang job)
<https://goplay.tools/>

Create a function that counts the word frequency in this string "Four, One two two three Three three four  four   four".  Case insensitive, ignore punctuation.

**Expected Answer (order doesn’t matter):**

**one => 1**

**two => 2**

**three => 3**

**four => 4**

**Code:**

**package main**

**import (**

`   `**"fmt"**

`   `**"regexp"**

`   `**"strings"**

**)**

**var nonAlphanumericRegex = regexp.MustCompile(`[^a-zA-Z0-9 ]+`)**

**func freqCount(s string) string {**

`   `**ret := ""**

`   `**s = strings.ToLower(nonAlphanumericRegex.ReplaceAllString(s, " "))**

`   `**wordsList := strings.Fields(s)**

`   `**wordsCount := make(map[string]int)**

`   `**for \_, word := range wordsList {**

`       `**\_, matched := wordsCount[word]**

`       `**if matched {**

`           `**wordsCount[word] += 1**

`       `**} else {**

`           `**wordsCount[word] = 1**

`       `**}**

`   `**}**

`   `**for k, v := range wordsCount {**

`       `**ret += fmt.Sprintf("%s => %d\n", k, v)**

`   `**}**

`   `**return ret**

**}**

**func main() {**

`   `**s := "Four,One two two three Three three four  four   four"**

`   `**fmt.Print(freqCount(s))**

**}**


# <a name="_40dvfcfd7qub"></a>
# <a name="_ruvan82do9tg"></a>Tools (Rate yourself 1 to 5)
- Git - 5
- Redis - 5
- VSCode - 5
- Linux - 4
- AWS - 1
  - EC2 - 1
  - Lambda - 1
  - RDS - 1
  - Cloudwatch - 1
  - S3 - 1
- Unit testing - 5
- Kanban boards - 3

