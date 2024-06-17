
ADELIA is based on Claire, tinyib, tinyboard, vichan, lynxchan, and fchannel. 






![Screenshot 2024-05-28 025835](https://github.com/ChessLogical/Adelia/assets/169053333/1d4d7ba9-3930-4921-a7b2-2d659470cb63)






TLDR-- Sqlite3 is decent, but it holds rust back. SO if you MUST use sqlite3 just feed this code to chatgpt and tell it what you need changed or edit to suit your needs. This a valuable learning tool or a starting point to make your own rust imageboard. I do not plan any further updates for this because sqlite3 and even sleddb holds rust back in terms of what rust is capable of. 
//////////////////////////////////////////////////////////////////////////////////////////////////////////

//////////////////////////////////////////////////////////////////////////////////////////////////


The message board application is a web-based platform designed to support around 100 individual boards, each dedicated to different topics or themes. Users can interact with these boards by creating new threads, posting messages, replying to existing posts, and uploading files such as images, videos, or documents.

Core Features
Multiple Boards: The application hosts multiple boards, each identified by a unique ID (e.g., /1, /2, etc.). Each board serves as a separate discussion space where users can post and view messages related to the board's specific topic.

Thread Creation: Users can start new threads on any board by submitting a form with a title, message, and optional file attachment. The thread becomes the root post of a new discussion within the board.

Post and Reply Functionality: Within each thread, users can reply to the original post or to other replies, creating a nested conversation structure. Each post can contain text and optional file attachments. Replies are linked to their parent posts, maintaining a clear hierarchy of discussions.

File Uploads: The application supports uploading various types of files, including images (JPEG, PNG, GIF, WEBP), videos (MP4, WEBM), and audio files (MP3). Uploaded files are stored in a central static directory and linked to their respective posts.

Dynamic Routing: The application uses dynamic routing to handle URLs for each board and post. For example, accessing /1 would display the content of board 1, while /1/post/123 would display a specific post with ID 123 on board 1. This dynamic routing allows the application to efficiently manage and display content for multiple boards without needing to create separate directories for each board.

Pagination: To handle large volumes of posts, the application implements pagination. This ensures that users can navigate through multiple pages of posts within a board, with a configurable number of posts displayed per page. Pagination links are dynamically generated based on the total number of posts and the current page.

Search and Retrieval: The application supports querying posts by board and retrieving posts along with their replies. This is essential for displaying threads and their associated replies correctly and efficiently.

Backend Operations
Database Management: The application uses a database (e.g., SQLite) to store all data related to boards, posts, replies, and file paths. Each post entry in the database includes fields for the post ID, parent ID (to link replies), title, message content, file path (if any), board ID, and timestamps for tracking the creation and last reply times.

Concurrency Handling: Given the potential for high user traffic, the application is designed to handle concurrent read and write operations efficiently. This ensures that multiple users can interact with the boards simultaneously without experiencing significant delays or performance issues.

Form Handling and Data Sanitization: When users submit forms to create or reply to posts, the application processes the form data, sanitizes the input to prevent security issues like SQL injection and cross-site scripting (XSS), and stores the sanitized data in the database.

Template Rendering: The application uses HTML templates to render the content dynamically. Templates include placeholders for dynamic data, such as post titles, messages, and file links, which are populated with actual data when rendering the page for the user.

User Experience
User-Friendly Interface: The application provides a user-friendly interface with clearly labeled buttons and forms for creating new threads and replying to existing posts. Navigation links and pagination controls make it easy for users to browse through posts and threads.

Responsive Design: The application is designed to be responsive, ensuring it works well on various devices, including desktops, tablets, and mobile phones. This enhances accessibility and usability for a wide range of users.

Backlinks and Navigation: Each post view includes a backlink to return to the main board or the parent thread, allowing users to navigate the application intuitively.

Overall, the message board application provides a robust platform for users to create, view, and interact with posts across multiple boards, with features designed to handle concurrent access and large volumes of data efficiently.


The application being developed is a sophisticated message board system designed to support around 100 individual boards, each dedicated to specific topics or themes. Users can create new threads, post messages, and upload files within these boards, with each board maintaining its own set of posts and replies. The system needs to handle create, read, update, and delete (CRUD) operations efficiently, as well as manage pagination to display posts in a user-friendly manner.

Concurrency is a significant concern, as the application is expected to handle multiple users accessing and interacting with the boards simultaneously. This requires a robust database system capable of managing concurrent read and write operations without significant performance degradation. The application also involves complex querying, such as retrieving posts by board, fetching replies to specific posts, and displaying posts with pagination, which necessitates a database that can handle relational data models effectively.

SQLite emerges as a suitable choice due to its mature relational database model, which supports complex queries, joins, and indexing. This makes it ideal for managing the relationships between posts and replies within the boards. SQLite's extensive documentation and community support add to its reliability, ensuring that any issues or questions can be addressed promptly. Additionally, using a single SQLite database simplifies data management tasks like backups and migrations.

On the other hand, Sled offers high performance and is designed for low-latency, concurrent operations, which can be beneficial for handling multiple boards with high traffic. However, Sled is a key-value store and lacks the advanced querying capabilities and relational data management features of SQLite. This would require adapting the data model to fit Sled's limitations, potentially complicating the development and maintenance of the application.

Given the application's need for complex data operations and the advantages of a relational database, SQLite is likely the superior choice. Optimizing SQLite with features like Write-Ahead Logging (WAL) and appropriate PRAGMA settings can enhance its performance and concurrency handling, making it well-suited to manage the application's requirements effectively.

