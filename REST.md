# REST

## REST API Best Practices
| **Category**                                                | **Best Practice**                                                                                                               | **Description**                                                          |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Use Nouns, Not Verbs**                                    | Use nouns for resource names (e.g., `/users`, `/orders`) instead of verbs (`/getUsers`)                                         | REST is resource-based; actions are determined by HTTP methods, not URLs |
| **HTTP Methods**                                            | Use proper HTTP verbs: GET (read), POST (create), PUT/PATCH (update), DELETE (remove)                                           | Follow HTTP semantics for clarity and interoperability                   |
| **Statelessness**                                           | Each request should contain all the information needed to process it                                                            | Server does not store client session state                               |
| **Use Plural Nouns**                                        | Use plural form for resource endpoints (`/books`, not `/book`)                                                                  | Consistency improves API readability and predictability                  |
| **Version Your API**                                        | Include version in the URI (e.g., `/api/v1/users`) or headers                                                                   | Allows backward-compatible changes without breaking clients              |
| **Use Meaningful HTTP Status Codes**                        | Return appropriate status codes: 200 OK, 201 Created, 204 No Content, 400 Bad Request, 404 Not Found, 500 Internal Server Error | Helps clients handle responses properly                                  |
| **Provide Useful Error Messages**                           | Include meaningful error details and codes in responses                                                                         | Helps clients understand and handle failures                             |
| **Use JSON as Default Format**                              | Prefer JSON for request/response bodies                                                                                         | Widely supported and easy to consume                                     |
| **Pagination, Filtering, Sorting**                          | Support pagination (`?page=2&size=10`), filtering (`?status=active`), and sorting (`?sort=createdAt`)                           | Efficiently handle large datasets                                        |
| **HATEOAS (Hypermedia as the Engine of Application State)** | Include links in responses to related resources                                                                                 | Helps clients navigate API dynamically                                   |
| **Security**                                                | Use HTTPS, implement authentication (OAuth, JWT), and authorization                                                             | Protect sensitive data and restrict access                               |
| **Rate Limiting**                                           | Limit number of requests per client to prevent abuse                                                                            | Protects your API and backend services                                   |
| **Use Consistent Naming**                                   | Stick to a naming convention (lowercase, hyphens or camelCase)                                                                  | Improves API usability and reduces confusion                             |
| **Documentation**                                           | Provide clear, up-to-date API documentation (Swagger/OpenAPI)                                                                   | Essential for developer adoption and usability                           |
| **Idempotency**                                             | Ensure safe methods (GET, PUT, DELETE) are idempotent                                                                           | Helps with retries and fault tolerance                                   |
| **Use Standard Media Types**                                | Use `application/json` and standard content types                                                                               | Ensures interoperability                                                 |

Here are some common approaches for naming resources with multiple words:
**1. Use Hyphens (Kebab Case)**
* Example: /user-accounts, /order-items, /payment-methods
* Why: Hyphens are easy to read and widely recommended by RESTful API guidelines (including Google API Design Guide).
* Best For: Public-facing APIs, where readability is crucial.
**2. Use CamelCase (PascalCase or camelCase)**
* Example: /userAccounts, /orderItems, /paymentMethods
* Why: Camel case is often used in programming languages, and can make URLs shorter. However, it's less readable than hyphens for longer phrases.
* Best For: Internal APIs or when following a convention already established in a codebase.
**3. Use Underscores (Snake Case)**
* Example: /user_accounts, /order_items, /payment_methods
* Why: Some developers prefer underscores for naming, especially in databases, but it’s less common for REST API resource URLs compared to hyphens.
* Best For: Specific team practices or legacy codebases that use underscores for naming.

Best Practice Resource Naming Recommendations:
* Hyphenated URLs (kebab-case) are the most common and recommended for readability and consistency.
* Avoid CamelCase or PascalCase for URLs, as they can be harder to read (e.g., /userAccounts vs /user-accounts).
* Consistency is Key: Choose a naming convention and stick with it throughout the API.

Examples of Resource Naming
| **Resource Type**       | **Recommended Name**   | **Explanation**                                                     |
| ----------------------- | ---------------------- | ------------------------------------------------------------------- |
| **User Accounts**       | `/user-accounts`       | Hyphenated for better readability and following standard convention |
| **Order Items**         | `/order-items`         | Clear and consistent with multiple words                            |
| **Payment Methods**     | `/payment-methods`     | Hyphenated for consistency and easier reading                       |
| **User Login Sessions** | `/user-login-sessions` | Hyphenated form for multi-word resources                            |
| **Product Details**     | `/product-details`     | Avoid using camelCase in URLs, use hyphens for better readability   |












