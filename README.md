
# eo.userClient
The `eo.userClient` collects and manages client-related data, including:
* User Agent: The client's browser user agent string.
* Geo Information: The client's location data (retrieved from ipinfo.io).
* Browser Detection: Determines the browser name based on the user agent.

This information is cached in localStorage to avoid redundant API calls.

* ## Usage Example
   ```javascript
   console.log(userClient.userAgent); // e.g., "Mozilla/5.0 (Windows NT 10.0; Win64; x64)..."
   console.log(userClient.geo); // e.g., { country: "US", city: "New York", ... }
   console.log(userClient.browser); // e.g., "Google Chrome"
   ```

* ## Properties
   userClient **Object**
   | Property | Type | Description |
   | --- | --- | --- |
   | `userAgent` | `string` | The browser's user agent string. |
   | `geo` | `Object` | null |
   | `browser` | `string` | string |

* ## Implementation Details
   **Fetching Geolocation Data**
   * If geolocation data isn't stored, userClient calls https://ipinfo.io/json to retrieve location details.
   * The response is cached in localStorage for future use.
   **Browser Detection**
   * Uses navigator.userAgent to determine the browser name.
   * Compares the user agent string against common browser signatures.

* ## Error Handling
   * Geo Fetch Failure: Logs an error (Error getting geo info:).
   * Unknown Browser: Defaults to "Unknown Browser" if no match is found.

# eo.redirect(url)
`eo.redirect(url)` navigates the browser to the specified URL by setting window.location.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `url` | `String` | The URL to which the browser should be redirected. |

* ## Returns
   `void` This function does not return anything. It redirects the user immediately.
* ## Example Usage
   ```javascript
   eo.redirect("https://example.com");
   // The browser navigates to "https://example.com"
   ```

# eo.epochToTimeString(epoch)
`eo.epochToTimeString(epoch)` converts a Unix epoch timestamp (seconds since 1970-01-01 UTC) into a human-readable date string formatted in US English.
Converts an epoch time (in seconds) to a localized string in the format: "Weekday, Month Day, Year, HH:MM AM/PM"

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `epoch` | `Number` | A **Unix timestamp** in **seconds** (not milliseconds). |

* ## Returns
   `String` A formatted date string in English (US locale).

* ## Example Usage
   ```javascript
   console.log(eo.epochToTimeString(1700000000)); 
   // Output: "Sunday, November 12, 2023, 12:26 PM"
   ```

# eo.trim(stringValue, maximumLength)
`eo.trim(stringValue, maxLength)` truncates a string if it exceeds the specified maxLength and appends "...". If the string is within the limit, it remains unchanged.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `stringValue` | `String` | The input string to be trimmed. |
   | `maxLength` | `Number` | The maximum allowed length of the string (including ... if truncated). |

* ## Returns
   `String` The original string if within maxLength, otherwise a truncated version with "..." appended.

* ## Example Usage
   ```javascript
   console.log(eo.trim("Hello, world!", 10)); 
   // Output: "Hello, w..."
   
   console.log(eo.trim("Short", 10)); 
   // Output: "Short" (unchanged)
   ```

# eo.formatFileSize(bytes, decimalPlaces = 0)
`eo.formatFileSize(bytes, decimalPlaces = 0)` converts a file size in bytes into a human-readable format (e.g., KB, MB, GB). It supports up to Yottabytes (YB) and allows formatting with a specified number of decimal places.

* ## Parameters
   | Parameter | Type | Default | Description |
   | --- | --- | --- | --- |
   | `bytes` | `Number` | Required | The file size in **bytes**. |
   | `decimalPlaces` | `Number` | `0` (optional) | The **number of decimal places** for formatting. |

* ## Returns
   `String` A human-readable file size with units (e.g., "1.5 MB", "500 KB").

* ## Example Usage
   ```javascript
   console.log(eo.formatFileSize(1024));       
   // Output: "1 KB"
   
   console.log(eo.formatFileSize(1048576));    
   // Output: "1 MB"
   
   console.log(eo.formatFileSize(1500000, 2)); 
   // Output: "1.50 MB"
   
   console.log(eo.formatFileSize(0));          
   // Output: "0 Bytes"
   ```

# eo.uuidv4()
`eo.uuidv4()` generates a random UUID (Universally Unique Identifier) Version 4 in the standard format:  
`xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`  
where x is a random hexadecimal digit and y is one of 8, 9, A, or B (per UUID v4 specification).

* ## Returns
   `String` A randomly generated UUID v4 in the format "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".

* ## Example Usage
   ```javascript
   console.log(eo.uuidv4()); 
   // Output: "3f94a8a7-1d2b-4c19-9b2f-6de8f0ea6df0" (random each time)
   ```

# eo.getRandomChar(length)
`eo.getRandomChar(length)` generates a random hexadecimal string of the specified length using the Web Crypto API for cryptographic security.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `length` | `Number` | The desired length of the output string. |

* ## Returns
   `String` A random hexadecimal string of the given length.

* ## Example Usage
   ```javascript
   console.log(eo.getRandomChar(10)); 
   // Output: "f3a9c2b4d1" (random each time)
   ```

# eo.getRandomNum(start, end)
`eo.getRandomNum(start, end)` generates a random integer between start and end (inclusive).

* ## Parameters
   | Parameter | Type | Default | Description |
   | --- | --- | --- | --- |
   | `start` | `Number` | Required | The minimum value (inclusive). |
   | `end` | `Number` | Required | The maximum value (inclusive). |

* ## Returns
   `Number` A random integer between start and end (both inclusive).

* ## Example Usage
   ```javascript
   console.log(eo.getRandomNum(1, 10)); 
   // Output: Random number between 1 and 10
   ```


# eo.convertCurrency(amount)
`eo.convertCurrency(amount)` formats large numbers into a more readable currency notation using suffixes like K (thousand), M (million), B (billion), T (trillion), and beyond, up to Googol (1e100).

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `amount` | `Number` \| `String` | The numeric value to be formatted. Can be a number or a string that represents a number. |

* ## Returns
   `String` A formatted string representing the number with an appropriate suffix (e.g., "1.5M", "2B").

* ## Example Usage
   ```javascript
   console.log(eo.convertCurrency(1500));      // "1.5K"
   console.log(eo.convertCurrency(1000000));   // "1M"
   console.log(eo.convertCurrency(2500000000)); // "2.5B"
   console.log(eo.convertCurrency(1e100));     // "1V"  (Googol)
   console.log(eo.convertCurrency(999));       // "999"
   ```

# eo.serializeFormData(formData)
`eo.serializeFormData(formData)` converts form data into a plain JavaScript object. It supports different input types, including:
**FormData** (browser API)  
**Array of object**s (e.g., { name: "email", value: "test@example.com" })  
**Plain JavaScript objects**  

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `formData` | `FormData` \| `Array` \| `Object` | The data to be converted into a plain object. |

* ## Returns
   `Object` A JavaScript object where keys represent form field names and values represent user input.

* ## Example Usage
   * **Handling FormData**
      ```javascript
      const formElement = document.querySelector("form");
      const formData = new FormData(formElement);
      
      console.log(eo.serializeFormData(formData));
      // { name: "John", email: "john@example.com", password: "123456" }
      ```
   
   * **Handling an Array of Objects**
      ```javascript
      const formArray = [
          { name: "username", value: "johndoe" },
          { name: "email", value: "john@example.com" }
      ];
      
      console.log(eo.serializeFormData(formArray));
      // { username: "johndoe", email: "john@example.com" }
      ```
   
   * **Handling a Plain Object**
      ```javascript
      const formObject = { age: 25, country: "USA" };
      
      console.log(eo.serializeFormData(formObject));
      // { age: 25, country: "USA" }
      ```

# eo.createHiddenInput(name, value)
`eo.createHiddenInput(name, value)` creates a hidden input field with a specified name and value. This is useful for storing data in forms without displaying it to the user.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `name` | `string` | The **name attribute** of the hidden input. |
   | `value` | `string` | The **value to be stored** in the hidden input. |

* ## Returns
   `HTMLElement` A hidden <input> element with the provided name and value.

* ## Example Usage
   * **Creating a Hidden Input**
   ```javascript
   const hiddenInput = createHiddenInput('user_id', '12345');
   document.body.appendChild(hiddenInput);
   ```
   * **Output**
      ```html
      <input type="hidden" name="user_id" value="12345">
      ```

* ## Error Handling
   | Error Condition | Thrown Error |
   | --- | --- |
   | `name` is **not a string** or empty | `"Invalid name"` |
   | `value` is **not a string** | `"Invalid value"` |

# eo.moveHtmlElement(fromSelector, toSelector)
`eo.moveHtmlElement(fromSelector, toSelector)` moves the inner HTML from one element to another. This is useful for dynamically repositioning content within a webpage.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `fromSelector` | `string` | **CSS selector** of the element whose content will be moved. |
   | `toSelector` | `string` | **CSS selector** of the element where the content will be placed. |

* ## Returns
   `void` Does not return a value. It modifies the DOM directly.

* ## Example Usage
   * **Move Content from One Element to Another**
      ```html
      <div id="source">
          <p>Hello, World!</p>
      </div>
      
      <div id="destination">
          <!-- Content will be moved here -->
      </div>
      ```
      ```javascript
      eo.moveHtmlElement('#source', '#destination');
      ```
      * **Output**
         ```html
         <div id="source">
             <!-- Empty after move -->
         </div>
         
         <div id="destination">
             <p>Hello, World!</p>
         </div>
         ```

# eo.post
The `eo.post` function **performs an HTTP POST request** to a specified `url` using the Fetch API. It supports **different data types** (`FormData`, `JSON`, `array`, or plain objects), **allows custom content types**, and provides **callback hooks** for different stages of the request.

* ## Syntax
   ```javascript
   eo.post(url, data, {
       onBeforeSend,
       onSuccess,
       onError,
       onComplete,
       contentType = 'application/x-www-form-urlencoded; charset=UTF-8'
   });
   ```

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `url` | `string` | The API endpoint where the request is sent. |
   | `data` | `FormData`, `Object`, `Array` | The data to be sent in the request body. |
   | `options` | `object` | Optional configuration options (see below). |
   * **Options Object**
      | Option | Type | Description |
      | --- | --- | --- |
      | `onBeforeSend` | `function` | **Callback function** executed before the request is sent. |
      | `onSuccess` | `function` | **Callback function** executed when the request is successful. |
      | `onError` | `function` | **Callback function** executed when the request fails. |
      | `onComplete` | `function` | **Callback function** executed when the request completes (whether successful or not). |
      | `contentType` | `string` | The `Content-Type` of the request (`application/json`, `application/x-www-form-urlencoded`, etc.). |

* ## Returns
   `void` Does not return a value. Instead, it executes the provided callback functions.

* ## Example Usage
   * **Send Form Data**
      ```javascript
      const formData = new FormData();
      formData.append('username', 'john_doe');
      formData.append('password', 'securePass123');
      
      eo.post('/login', formData, {
          onSuccess: (response) => console.log('Login Success:', response),
          onError: (xhr, status, error) => console.error('Error:', status, error)
      });
      ```
   
   * **Send JSON Data**
      ```javascript
      const userData = { username: 'john_doe', age: 30 };
      
      eo.post('/update-profile', userData, {
          contentType: 'application/json',
          onSuccess: (response) => console.log('Profile Updated:', response),
          onError: (xhr, status, error) => console.error('Profile Update Failed:', error)
      });
      ```

# eo.get
The `eo.get` function **performs an HTTP GET request** to fetch data from a given `url`. It supports **callbacks for request lifecycle events**, including `beforeRequest`, `onSuccess`, and `onError`. The function **automatically detects and processes JSON responses** while handling errors gracefully.

* ## Syntax
   ```javascript
   eo.get(url, { beforeRequest, onSuccess, onError });
   ```

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `url` | `string` | The API endpoint from which data is fetched. |
   | `options` | `object` | (Optional) An object containing callback functions (see below). |
   * **Options Object**
      | Option | Type | Description |
      | --- | --- | --- |
      | `beforeRequest` | `function` | **Callback function** executed before the request is made. If it returns `false`, the request is canceled. |
      | `onSuccess` | `function` | **Callback function** executed when the request is successful. Receives the response data as an argument. |
      | `onError` | `function` | **Callback function** executed when the request fails. Receives (`null`, `'error'`, `error`) as arguments. |

* ## Returns
   `Promise<any>` A promise that resolves with the response data or logs an error.

* ## Example Usage
   * **Basic GET Request**
      ```javascript
      get('/api/user', {
          onSuccess: (data) => console.log('User Data:', data),
          onError: (xhr, status, error) => console.error('Error:', status, error)
      });
      ```
   * **Cancel Request with** `beforeRequest`
      ```javascript
      get('/api/config', {
          beforeRequest: () => {
              console.log('Checking before request...');
              return false; // Request will be canceled
          },
          onSuccess: (data) => console.log('Config Loaded:', data),
      });
      ```
# eo.createElements(tag, attributes = {}, children)
`eo.createElements(tag, attributes, children)` dynamically creates an HTML element, applies attributes, and appends child elements or text nodes. Ensures data sanitization before inserting into the DOM.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `tag` | `string` | The **HTML tag name** (e.g., `'div'`, `'span'`). |
   | `attributes` | `object` (optional) | An object containing **attribute key-value pairs** (e.g., `{ class: 'btn', id: 'my-button' }`). |
   | `children` | `array` (optional) | An array of **child elements or strings** (text content). |

* ## Returns
   `HTMLElement` Returns a newly created DOM element with the specified attributes and children.

* ## Example Usage
   * **Creating a Simple** `<div>`
      ```javascript
      const div = eo.createElements('div', { class: 'container', id: 'main' }, ['Hello, world!']);
      document.body.appendChild(div);
      ```
      * **Output**
         ```html
         <div class="container" id="main">Hello, world!</div>
         ```
   
   * **Creating a Nested Structure**
      ```javascript
      const button = eo.createElements('button', { class: 'btn', type: 'button' }, ['Click Me']);
      const wrapper = eo.createElements('div', { class: 'wrapper' }, [button]);
      
      document.body.appendChild(wrapper);
      ```
      * **Output**
         ```html
         <div class="wrapper">
             <button class="btn" type="button">Click Me</button>
         </div>
         ```

* ## Error Handling
   | Error Condition | Thrown Error |
   | --- | --- |
   | `tag` is **not a string** or empty | `"Invalid tag name"` |
   | `attributes` is not an object | `"Attributes must be an object"` |
   | `children` is not an array | `"Children must be an array"` |

# eo.alert
To use the `eo.alert`, ensure the necessary HTML structure includes a container for displaying alerts.
* ## Required HTML Structure
   ```html
   <div class="response"></div>
   ```
   This will act as the default container for displaying alerts and loaders.
* ## Methods
   * ### success(message, element) and error(message, element)
      Displays a success alert.
      | Parameter | Type | Default | Description |
      | --- | --- | --- | --- |
      | `message` | `String` | *required* | The success message. |
      | `element` | `String` | *optional*, `default: '.response'` | The container where the alert will be displayed. |
      * #### Example Usage
         ```javascript
         eo.alert.success('Operation completed successfully!');
         eo.alert.error('An error occurred while processing your request.');
         ```
   * ### loader(message, element)
      Displays a processing loader with a message.
      | Parameter | Type | Default | Description |
      | --- | --- | --- | --- |
      | `message` | `String` | *optional*, `default: 'Processing, Please wait...'` | The success message. |
      | `element` | `String` | *optional*, `default: '.response'` | The container where the alert will be displayed. |
      * #### Example Usage
         ```javascript
         eo.alert.loader();
         eo.alert.loader('Uploading file, please wait...');
         ```

# eo.modal
The `eo.modal` provides an easy way to create and manage Bootstrap modals dynamically. It supports custom modal sizes, dynamic content injection, and automatic cleanup of destroyable modals.

* **Features**
   * Dynamically create modals with custom sizes.
   * Inject content into the modal using a callback function.
   * Support for modals with status indicators.
   * Automatic destruction of modals when closed (if enabled).
   * Handles modal close events properly.

* **Notes**
   * Ensure Bootstrap is loaded for this to function properly.
   * The callback function should return a valid HTML string or a DOM element.
   * Destroyable modals are automatically removed from the DOM upon closing.

* ## Methods
   * ### create({ id, size, callback, status = false, destroyable = true })
      Creates and displays a Bootstrap modal.
      
      * #### Parameters
         | Parameter | Type | Default | Description |
         | --- | --- | --- | --- |
         | `id` | `String` | *required* | The unique ID of the modal. |
         | `size` | `String` | *required* | Modal size (`xs`, `sm`, `md`, `lg`, `xl`, `fullscreen`). |
         | `callback` | `Function` | *optional* | A function returning the modal content (HTML string or DOM element). |
         | `status` | `Boolean` | *optional*, `default: false` | If true, adds a status indicator inside the modal. |
         | `destroyable` | `Boolean` | *optional*, `default: true` | If true, the modal will be removed from the DOM after closing. |
      
      * #### Example Usage
         ```javascript
         eo.commponent.modal.create({
           id: 'exampleModal',
           size: 'md',
           callback: () => '<p>This is a dynamic modal!</p>',
           status: 'success',
           destroyable: true
         });
         ```

# eo.button
The `eo.button` provides utility functions to enable or disable buttons (or any clickable elements) dynamically. It ensures a smooth user experience by preventing interactions when necessary (e.g., during form submission or loading states).

* ## Methods
   * ### disable(selector = '.btn')
      Disables all buttons (or specified elements) by:
      * Changing the cursor to "wait".
      * Disabling pointer events.
      * Reducing opacity to indicate inactivity.
      * Disabling the button element.
      
      * #### Parameters
         | Parameter | Type | Default | Description |
         | --- | --- | --- | --- |
         | `selector` | `String` | *optional* `defaults: '.btn'` | The CSS selector of the elements to disable.|
      
      * #### Example Usage
         ```javascript
         eo.button.disable(); // Disables all buttons with class '.btn'
         eo.button.disable('.custom-button'); // Disables elements with class '.custom-button'
         ```
   
   * ### enable(selector = '.btn')
      Re-enables previously disabled buttons (or elements) by:
      * Resetting the cursor to default.
      * Restoring pointer events.
      * Restoring opacity.
      * Enabling the button element.
      
      * #### Parameters
         | Parameter | Type | Default | Description |
         | --- | --- | --- | --- |
         | `selector` | `String` | *optional* `defaults: '.btn'` | The CSS selector of the elements to enable.|
      
      * #### Example Usage
         ```javascript
         button.enable(); // Enables all buttons with class '.btn'
         button.enable('.custom-button'); // Enables elements with class '.custom-button'
         ```
         
# eo.getYoutubeVideoData(url)
`eo.getYoutubeVideoData(url)` extracts YouTube video details from a given URL.
It retrieves:  
* **The video ID**
* **Thumbnail URLs** in various resolutions
* The **direct watch URL**
* The **embed URL**

If the URL is invalid, an error alert is triggered.

* ## Parameters
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `url` | `string` | The YouTube video URL to extract details from. |

* ## Returns
   | Type	| Description |
   | --- | --- |
   | `Object`	| Returns an object with video details (**if the URL is valid**). |
   | `null`	| Returns null and triggers an alert if the URL is invalid. |

* ## Example Usage
   * **Valid Youtube URL**
      ```javascript
      const videoData = eo.getYoutubeVideoData("https://www.youtube.com/watch?v=dQw4w9WgXcQ");
      
      console.log(videoData);
      /* {
        id: "dQw4w9WgXcQ",
        thumbnail: {
          default: "http://img.youtube.com/vi/dQw4w9WgXcQ/default.jpg",
          hq: "http://img.youtube.com/vi/dQw4w9WgXcQ/hqdefault.jpg",
          mq: "http://img.youtube.com/vi/dQw4w9WgXcQ/mqdefault.jpg",
          sd: "http://img.youtube.com/vi/dQw4w9WgXcQ/sddefault.jpg",
          maxres: "http://img.youtube.com/vi/dQw4w9WgXcQ/maxresdefault.jpg",
        },
        url: "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
        embed: "https://www.youtube.com/embed/dQw4w9WgXcQ"
      } */
      ```
   
   * **Invalid YouTube URL**
      ```javascript
      const videoData = eo.getYoutubeVideoData("https://example.com/video");
      
      console.log(videoData); // null
      // ⚠️ Alert: "Invalid YouTube URL"
   ```

* ## Supported Youtube URL Formats
   | Format Type | Example |
   | --- | --- |
   | Standard URL | https://www.youtube.com/watch?v=**VIDEO_ID** |
   | Shortened URL | https://youtu.be/**VIDEO_ID** |
   | Embed URL | https://www.youtube.com/embed/**VIDEO_ID** |
   | Other Variants | https://www.youtube.com/v/**VIDEO_ID**, https://www.youtube.com/watch?v=**VIDEO_ID**&feature=share |

# eo.video
The Video Component is for managing YouTube videos within a web interface. It provides functionalities to:
* Add a YouTube video by URL.
* Play the video in a modal.
* Remove added videos.
* Create a hidden input dynamically.
   * `id`, `url`, `embed`, `thumbnail`, and `created_at`
   
* ## Usage
   Call `eo.video.init()` before the page loads.
   ```javascript
    window.addEventListener('load', () => {
       eo.video.init();
    });
   ```
* ## Required HTML Structure
   To integrate the video module, add the following HTML elements:
   ```html
   <div class="response"></div>
   <div id="videoInput"></div>
   <div class="video-list-container"></div>
   ```
   * ### Description
      * **.response** - Displays messages after adding a video.
      * **#videoInput** - The container where the input field and add button will be appended.
      * **.video-list-container** - The section where added videos will be listed.
      * Clicking on an added video will play it in a fullscreen modal.
      * A delete button is provided to remove a video entry.

# **eo.validator**
The `eo.validator` is a lightweight data validation utility that checks objects against predefined rules. It supports nested properties using dot notation and provides customizable validation rules and error messages.

* **Features**
   * Validates objects based on predefined constraints.
   * Supports nested properties using dot notation.
   * Customizable validation rules.
   * Customizable error messages.

* ## Usage Example
   ```javascript
   const rules = {
     name: { required: true, length: { min: 3, max: 50 } },
     email: { required: true, email: true },
     age: { number: { min: 18, max: 99 } },
     address: { 
       street: { required: true }, 
       city: { required: true }
     }
   };
   
   eo.validator.setConstraints(rules);
   
   const data = {
     name: "John",
     email: "invalid-email",
     age: 17,
     address: { street: "123 Main St" }
   };
   
   if (!eo.validator.validate(data)) {
     console.log(eo.validator.getErrors()); 
     // Output: [ "Email is not a valid email address.", "Age must be a number greater than 18.", "Address City is required." ]
   }
   ```
* ## Methods
   * ### `validate(data, rules)`
   
      Validates the given data object against rules and collects errors.  
      **Parameters:**
      * `data` (Object) – The object to validate.
      * `rules` (Object, optional) – The validation rules. If omitted, previously set constraints are used.
      
      **Returns:**
      * `true` if validation passes.
      * `false` if validation fails (errors can be retrieved using getErrors()).
      
      **Example:**
      ```javascript
      const isValid = eo.validator.validate({ name: "Alice" });
      console.log(isValid); // true or false
      ```
   * ### `getErrors()`
   
      Retrieves an array of validation errors from the last `validate()` call.  
      **Returns:**
      * `Array<String>` – A list of human-readable error messages.
      
      **Example:**
      ```javascript
      console.log(eo.validator.getErrors());
      // Output: [ "Email is not a valid email address." ]
      ```
   * ### `setConstraints(rules)`
      Sets default validation rules to be used for all future validations.
      
      **Parameters:**
      * `rules (Object)` – The validation rules object.
      
      **Example:**
      ```javascript
      eo.validator.setConstraints({ username: { required: true } });
      ```
   * ### `resetConstraints()`
   
      Clears all previously set validation rules.
      
      **Example:**
      ```javascript
      eo.validator.resetConstraints();
      ```
* ## Validation Rules
   The validator supports various rules that can be applied to fields.
   
   | Rule | Parrameter Type | Description |
   | --- | --- | --- |
   | `required` | `Boolean` | Ensures a value is present (not `null`, `undefined`, or empty). |
   | `length` | `{ min, max }` | Enforces string length constraints. |
   | `number` | `{ min, max }` | Ensures a value is a number and optionally within a range. |
   | `url` | `Boolean` | Ensures a valid URL format (http:// or https://). |
   | `email` | `Boolean` | Ensures a valid email format. |
   | `date` | `Boolean` | Ensures a valid date format (`YYYY-MM-DD`). |
   | `datetime` | `Boolean` | Ensures a valid datetime format. |
   | `equality` | `Any` | Ensures the value matches the given parameter exactly. |
   | `type` | `String` | Ensures the value is of the specified JavaScript type (`string`, `number`, etc.). |
   
   **Example Rule Definition:**
   ```javascript
   const rules = {
     name: { required: true, length: { min: 3, max: 50 } },
     email: { required: true, email: true },
     age: { number: { min: 18, max: 99 } },
     brithdate: { date: true }
     address: { 
       street: { required: true }, 
       city: { required: true }
     }
   };
   ```

   **Custom Error Messages**
   Custom error messages can be defined in the constraints. If a custom message is provided, it will be used instead of the default error message.
   
   * **Example Usage with Custom Messages**
      ```javascript
      const constraints = {
       first_name: {
           required: { param: true, message: 'cannot be empty.' },
           length: { min: 2, max: 50, message: 'should have 2 to 50 characters.' }
       },
       email: {
           required: { param: true, message: 'is needed for account creation.' },
           email: { param: true, message: 'must be a valid email format.' }
       }
      };
      ```


# eo.tinymce
The TinyMCE Module provides an easy way to initialize and configure TinyMCE, a popular WYSIWYG editor, on a specified container. It ensures the script is included and allows overriding default settings.

* **Features**
* **Initialize TinyMCE** on a specified `<textarea>` element.
* **Merge default options** with custom options for flexibility.
* **Ensure TinyMCE is removed before initialization** to prevent duplicates.

* ## Required Setup
   Ensure that the TinyMCE script is included in your project. If missing, an error will be thrown.
   ```html
   <script src="https://cdn.tiny.cloud/1/no-api-key/tinymce/6/tinymce.min.js"></script>
   ```
   > for more information about TinyMCE, please visit their [website](https://www.tiny.cloud/docs/tinymce/latest/)
   
   * ## Method
      * ### init(containerId, options)
         Initializes TinyMCE on the specified textarea.
         
         * #### Parameters
            | Parameter | Type | Description |
            | --- | --- | --- |
            | `containerId` | `string` | The ID or class selector of the textarea (e.g., `#editor`). |
            | `options` | `object` | (Optional) Custom TinyMCE configuration options. |
            
            * ##### Default Options
               The module applies the following default configuration:
               ```javascript
               {
                   selector: `textarea${containerId}`,
                   height: 500,
                   menubar: false,
                   plugins: ['advlist lists link anchor', 'media table paste code'],
                   content_css: [
                       'https://fonts.googleapis.com/css?family=Lato:300,300i,400,400i's
                   ]
               }
               ```
               If you need to customize the options, pass an object to override specific settings.

* ## Example Usage
   * **Basic Initialization**
      ```javascript
      tinymce.init('#editor');
      ```
   * **Custom Configuration**
      ```javascript
      tinymce.init('#editor', {
          height: 300,
          plugins: ['lists', 'table', 'code'],
          toolbar: 'bold italic | alignleft aligncenter alignright'
      });
      ```

# eo.googleChart
This `eo.googleChart` simplifies the integration of Google Charts by providing methods for various chart types.

* ## Required Setup
   Ensure you have included the Google Charts script in your HTML:
   ```html
   <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
   ```
   * **Documentation**
      For DataTable and Chart Configuration please read [Google Chart Documentation](https://developers.google.com/chart/interactive/docs/quick_start)

* ## Common Parameters
   All chart functions accept the following parameters:
   | Parameter | Type | Description |
   | --- | --- | --- |
   | `containerId` | `string` | The ID of the HTML element where the chart will be rendered. |
   | `data` | `function(DataTable)` | A function that returns a populated `google.visualization.DataTable` object. |
   | `options` | `object` | (Optional) Chart-specific configuration options. |
   | `apiKey` | `string` | (Optional, required for Geo and Map charts) Google API key for maps/geolocation features. |

* ## Available Methods
   1. ### `googleChart.bar(params)`
      Renders a bar chart.
      
      * #### Example Usage
         ```javascript
         googleChart.bar({
             containerId: 'barChart',
             data: (dataTable) => {
                 dataTable.addColumn('string', 'Year');
                 dataTable.addColumn('number', 'Sales');
                 dataTable.addRows([ ['2020', 1000], ['2021', 1500] ]);
                 return dataTable;
             },
             options: { title: 'Annual Sales' }
         });
         ```
   
   2. ### `googleChart.calendar(params)`
      Renders a calendar heatmap chart.
      
      * #### Example Usage
         ```javascript
         googleChart.calendar({
             containerId: 'calendarChart',
             data: (dataTable) => {
                 dataTable.addColumn({ type: 'date', id: 'Date' });
                 dataTable.addColumn({ type: 'number', id: 'Sales' });
                 dataTable.addRows([ [new Date(2024, 0, 1), 100], [new Date(2024, 1, 14), 200] ]);
                 return dataTable;
             }
         });
         ```
   
   3. ### `googleChart.geo(params)`
      Renders a geographical map chart.
      > ⚠️ **Requires an API key for** `displayMode: 'markers'`.
      
      * #### Example Usage
         ```javascript
         googleChart.geo({
             containerId: 'geoChart',
             data: (dataTable) => {
                 dataTable.addColumn('string', 'Country');
                 dataTable.addColumn('number', 'Population');
                 dataTable.addRows([ ['Germany', 83000000], ['France', 67000000] ]);
                 return dataTable;
             },
             options: { displayMode: 'markers' },
             apiKey: 'YOUR_GOOGLE_MAPS_API_KEY'
         });
         ```
   
   4. ### `googleChart.pie(params)`
      Renders a pie chart.
      
      * #### Example Usage
         ```javascript
         googleChart.pie({
             containerId: 'pieChart',
             data: (dataTable) => {
                 dataTable.addColumn('string', 'Category');
                 dataTable.addColumn('number', 'Value');
                 dataTable.addRows([ ['Electronics', 40], ['Clothing', 25], ['Groceries', 35] ]);
                 return dataTable;
             },
             options: { title: 'Sales Breakdown' }
         });
         ```
   
   5. ### `googleChart.line(params)`
      Renders a line chart.
      
      * #### Example Usage
         ```javascript
         googleChart.line({
             containerId: 'lineChart',
             data: (dataTable) => {
                 dataTable.addColumn('string', 'Month');
                 dataTable.addColumn('number', 'Revenue');
                 dataTable.addRows([ ['Jan', 5000], ['Feb', 7000], ['Mar', 6000] ]);
                 return dataTable;
             },
             options: { title: 'Monthly Revenue' }
         });
         ```
   
   6. ### `googleChart.map(params)`
      Renders a Google Maps visualization.
      > ⚠️ **Requires an API key.**
      
      * #### Example Usage
         ```javascript
         googleChart.map({
             containerId: 'mapChart',
             data: (dataTable) => {
                 dataTable.addColumn('number', 'Lat');
                 dataTable.addColumn('number', 'Lng');
                 dataTable.addColumn('string', 'Label');
                 dataTable.addRows([ [37.7749, -122.4194, 'San Francisco'], [40.7128, -74.0060, 'New York'] ]);
                 return dataTable;
             },
             options: { showTooltip: true, showInfoWindow: true },
             apiKey: 'YOUR_GOOGLE_MAPS_API_KEY'
         });
         ```
   
   7. ### `googleChart.trendLine(params)`
      Renders a scatter plot with a trend line.s
      
      * #### Example Usage
         ```javascript
         googleChart.trendLine({
             containerId: 'trendChart',
             data: (dataTable) => {
                 dataTable.addColumn('number', 'X');
                 dataTable.addColumn('number', 'Y');
                 dataTable.addRows([ [1, 2], [2, 4], [3, 6], [4, 8] ]);
                 return dataTable;
             },
             options: { trendlines: { 0: {} } }
         });
         ```

* ## Error Handling
   * If the `containerId` is invalid, the function will return `false`.
   * If `data` is missing, an error will be thrown:
      ```javascript
      Error: Set the data in table property
      ```
   * For geo and map charts, an API key is required. If missing, an error will be thrown
      ```javascript
      Error: Maps require a mapsApiKey.
      ```

# EO.js Components
* ## eo.submitForm
   The `eo.submitForm` simplifies handling form submissions, including validation, AJAX posting, and success/error handling. It integrates with the `eo.validator` for form validation
   
   * **Features**
      * Validates form data using the `eo.validator` before submission.
      * Submits form data via AJAX (`post` function).
      * Displays alerts using the `eo.alert`.
      * Handles success and error responses.
      * Disables & enables buttons during the request to prevent multiple submissions.
      * Redirects users upon success if `redirectUrl` is provided.
   
   * **Dependencies**
      * eo.validator (Read the documentation)
      * eo.post (Read the documentation)
	  * eo.alert (Read the documentation)
	  * eo.button (Read the documentation)
	  * csrf-token in meta tag
	     ```html
		 <meta name="csrf-token" content="{{ csrf_token() }}">
		 ```
   
   * ### Syntax
      ```javascript
      eo.submitForm(formId, { validation, callback, onBeforeSend, redirectUrl } = {})
      ```
   
   * ### Parameters
      | Parameter | Type | Description |
      | --- | --- | --- |
      | `formId` | `string` | The ID of the form to submit (with or without `#`). |
      | `validation` | `object` | The validation rules based on the eo.validator (read the documentation). |
      | `callback` | `function` | A callback function executed on a successful submission. |
      | `onBeforeSend` | `function` | A function executed before sending the form data. |
   
   * ### Example Usage
      ```javascript
      eo.submitForm('#myForm', {
          validation: {
              name: { required: true, min: 3 },
              email: { required: true, email: true },
          },
          callback: (formData, response) => {
              console.log('Form submitted successfully:', response);
          },
          onBeforeSend: (formData) => {
              console.log('Processing form data:', formData);
          },
          redirectUrl: '/dashboard'
      });
      ```

* ## eo.mortgageCalculator
   The `eo.mortgageCalculator` provides functionalities to calculate monthly mortgage payments, create selection elements for down payment    interest rates, and loan years, and display the results. It is designed to be embedded into a mortgage calculator form on a web page.
   
   **Notes**
   * Ensure that the form elements (#sellingPrice, #dpSelection, #interestSelection, #yearSelection, and #result) exist in your HTML.
   * The script should be included and initialized correctly to work as expected.
   * Customize the form and style as needed to fit your design.
      
   * ### Required Setup
      Ensure to call the `eo.mortgageCalculator.init()` method to create the necessary selection elements and calculate the initial mortgage payment.
      * #### JavaScript
         ```javascript
         window.addEventListener('load', () => {
             eo.mortgageCalculator.init();
         });
         ```
      * #### Html
         ```html
         <div class="mortgage-calculator-form">
             <input type="text" id="sellingPrice" placeholder="Enter Selling Price"> /* you can change the type to hidden */
             <div id="dpSelection"></div>
             <div id="interestSelection"></div>
             <div id="yearSelection"></div>
             <div id="result"></div>
         </div>
            ```

* ## eo.uploader
   The `eo.uploader` provides an easy-to-use interface for uploading images and documents with preview functionality. It supports both single and multiple file uploads, customizable options, and callback hooks for different stages of the upload process.
   
   **Features**
   * Supports image and document uploads.
   * Provides preview functionality for uploaded files.
   * Supports single and multiple file uploads.
   * Customizable options for upload type, file acceptance, and event callbacks.
   * Automatically handles UI creation and event binding.
   
   * ### Setup
      **Required HTML Structure:**

	  Container for the response.
      ```html
      <div class="response"></div>
      ```
      
      Container for the upload button.
      ```html
      <div class="upload-container"></div>
      ```
      
      Container for the preview of uploaded files.
      ```html
      <div class="uploaded-photo"></div>
      ```
      
      Initializes the uploader with specified configuration and attaches necessary event listeners.
      ```javascript
      uploader.create('.upload-container', '/upload-url', {
         inputName: 'eoFileUpload',
         previewSelector: '.uploaded-photo',
         disablePreview: false,
         uploadType: 'image',
         accept: 'image/*',
         multiple: true,
         onBeforeSend: () => { console.log('Before sending the request'); },
         onSuccess: (response, files) => {
             console.log('Upload successful!', response, files);
             files.forEach((file, index) => {
                 // Manipulate hidden input value, e.g., add a URL property
                 file.url = response[index].url; // Assuming response contains URLs for each file
                 console.log(`File ${index + 1} URL: ${file.url}`);
             });
         },
         onError: (error) => { console.error('Upload failed!', error); }
      });
      ```
   
      * ### Parameters
         | Parameters | Type | Default | Description |
         | --- | --- | --- | --- |
         | `uploadSelector` | `String` | `required` | CSS selector for the upload container. |
         | `url` | `String` | `required` | The endpoint URL where the files will be uploaded. |
         | `options` | `Object` | `optional` | Configuration options for the uploader. |
      
         * #### Options
            | Parameter | Type | Default | Description |
            | --- | --- | --- | --- |
            | `inputName` | `String` | `eoFileUpload` | The input name. |
            | `previewSelector` | `String` | `.uploaded-photo` | CSS selector for the preview container. |
            | `disablePreview` | `Boolean` | `false` | Whether to disable the preview functionality. |
            | `uploadType` | `String` | `image` | Type of upload (`image` or `document`). |
            | `accept` | `String` | `image/*` for images and `application/pdf` for documents | File types to accept. |
            | `multiple` | `Boolean` | `true` | Whether to allow multiple file uploads. |
            | `onBeforeSend` | `Function` | `optional` | Callback function before the upload request is sent. |
            | `onSuccess` | `Function` | `optional` | Callback function on successful upload. |
            | `onError` | `Function` | `optional` | Callback function on upload error. |
      
         * #### onSuccess Example:
            ```javascript
            onSuccess: (response, files) => {
                files.forEach((file, index) => {
                    // Manipulate hidden input value
                   file.url = response[index].url; // Assuming response contains URLs for each file
                });
            }
            ```
            1. `onSuccess` **Callback**: This function is called when the upload is successful.
            2. **Iterating through Files**
               * The `files` array contains the uploaded file objects.
               * The `forEach` method is used to iterate through each file.
            3. **Updating File Properties**
               * Inside the loop, a new property `url` is added to each file object.
               * The `url` property is assigned a value (e.g., `'https://your-assigned-url-from-server-response.com'`).
               * This URL can be dynamically assigned based on your requirements.
            
            **Hidden Input Creation**
            The uploader module automatically creates hidden inputs for each file property (`name`, `size`, `type`, `lastModified`, etc.).
            **Image-Specific Properties**
            If the upload type is `image`, the module also creates hidden inputs for the image's `width` and `height`.
            
            By using the onSuccess callback, you can dynamically manipulate the files array and update properties based on your requirements. This ensures that you have full control over the file objects after a successful upload.
   
   * ### Comprehensive Guide
      * **First Scenario**  
         In this scenario, you upload an image, process it, move it to a temporary folder, and return the image data in JSON format. Upon a    successful response, hidden input fields are dynamically created based on the server’s response. Finally, submit your form to save the    image data to the database.
         
         1. **Create a `<form>` Tag**:
            ```html
            <form id="uploadForm" action="/submit-form-url" method="post">
                <div class="response"></div>
                <div class="upload-container"></div>
                <div class="uploaded-photo"></div>
                <button type="submit">Submit</button>
            </form>
            ```
         2. **Initialize the Uploader:**
            ```javascript
            uploader.create('.upload-container', '/upload-file-url', {
               inputName: 'eoFileUpload',
               previewSelector: '.uploaded-photo',
               disablePreview: false,
               uploadType: 'image',
               accept: 'image/*',
               multiple: true,
               onBeforeSend: () => { console.log('Before sending the request'); },
               onSuccess: (response, files) => {
                   files.forEach((file, index) => {
                       // Manipulate hidden input value
                      file.url = response[index].url; // Assuming response contains URLs for each file
                   });
               },
               onError: (error) => { console.error('Upload failed!', error); }
            });
            ```
         3. **Uploader Creates a Form:** The uploader will create a form inside the `<body>` tag and handle file selection and submission.
         4. **Access the File on the Server Side:**
            ```php
            header('Content-Type: application/json; charset=utf-8');
            if ($_SERVER['REQUEST_METHOD'] === 'POST') {
               // if multiple file upload was used, the $_FILES array has a different structure,
               // so you need first to re-structure it so it can be looped through
               $files = array(); 
               foreach ($_FILES['eoFileUpload'] as $k => $l) {
                  foreach ($l as $i => $v) {
                     if (!array_key_exists($i, $files)) $files[$i] = array();
                     $files[$i][$k] = $v;
                  }
               }

               foreach ($files as $key => $file) {
                  // Move file to the desired folder
                  $file_data['name'] = basename($file[$key]['name']);
                  $file_data['url'] = "https://your-domain.com/images/" . $file_data['name'];
                  move_uploaded_file($file[$key]['tmp_name'], '/temporary/' . $file_data['name']);
               }

               echo json_encode($file_data);

               /**
                * for single upload
                * Example: move_uploaded_file($_FILES['eoFileUpload']['tmp_name'], '/temporary/' . $file_data['name']);
               */
            }
            ```
         5. **Manipulate Hidden Input Values Based on Response:**
            ```javascript
            onSuccess: (response, files) => {
               console.log('Upload successful!', response, files);
               files.forEach((file, index) => {
                  // Access and manipulate the hidden input values based on the response
                  // Example: add URL property
                  file.url = response[index].url; // Assuming response contains URLs for each file
                  // Example: update NAME property
                  file.name = response[index].name; // Assuming response contains Name for each file
               });
            }
            ```
            Created hidden input after successful upload.
            ```html
            <input type="hidden" name="upload[4CN44n6AAtK][name]" value="example.jpg">
            <input type="hidden" name="upload[4CN44n6AAtK][size]" value="102400">
            <input type="hidden" name="upload[4CN44n6AAtK][type]" value="image/jpeg">
            <input type="hidden" name="upload[4CN44n6AAtK][lastModified]" value="1633024800000">
            <input type="hidden" name="upload[4CN44n6AAtK][width]" value="800">
            <input type="hidden" name="upload[4CN44n6AAtK][height]" value="600">
            <input type="hidden" name="upload[4CN44n6AAtK][url]" value="https://your-assigned-url-from-server-response.com">
            ```
         6. **Submit Your Form**
         7. **Access the Hidden Input on the Server Side:**
		    After submitting the form, the hidden inputs created by the uploader module can be accessed on the server side using `$_POST['upload']`.
            ```php
            if ($_SERVER['REQUEST_METHOD'] === 'POST') {
                // Loop through each uploaded file's information
                foreach ($_POST['upload'] as $file_id => $file_info) {
                    $name = $file_info['name'];
                    $size = $file_info['size'];
                    $type = $file_info['type'];
                    $lastModified = $file_info['lastModified'];
                    $width = isset($file_info['width']) ? $file_info['width'] : null;
                    $height = isset($file_info['height']) ? $file_info['height'] : null;
            
                    // Process the file information as needed
                    echo "File ID: $file_id\n";
                    echo "Name: $name\n";
                    echo "Size: $size bytes\n";
                    echo "Type: $type\n";
                    echo "Last Modified: " . date('Y-m-d H:i:s', $lastModified / 1000) . "\n";
                    echo "Width: $width px\n";
                    echo "Height: $height px\n";
                }
            }
            ```
      * **Second Scenario**  
         In this scenario, you upload an image, process its data, move the image to a directory, and save it in the database.
         1. **Include Required HTML Tags:**
            ```html
            <div class="response"></div>
            <div class="upload-container"></div>
            <div class="uploaded-photo"></div>
            ```
         2. **Initialize the Uploader:**
            ```javascript
            uploader.create('.upload-container', '/upload-file-url', {
               inputName: 'eoFileUpload', // give the input file a name
               previewSelector: '.uploaded-photo',
               disablePreview: false,
               uploadType: 'image',
               accept: 'image/*',
               multiple: true,
               onBeforeSend: () => { console.log('Before sending the request'); }
               onError: (error) => { console.error('Upload failed!', error); }
            });
            ```
         3. **Uploader Creates a Form:** The uploader will create a form inside the `<body>` tag and handle file selection and submission.
         4. **Access the File on the Server Side:**
            ```php
            if ($_SERVER['REQUEST_METHOD'] === 'POST') {
               // if multiple file upload was used, the $_FILES array has a different structure,
               // so you need first to re-structure it so it can be looped through
               $files = array(); 
               foreach ($_FILES['eoFileUpload'] as $k => $l) {
                  foreach ($l as $i => $v) {
                     if (!array_key_exists($i, $files)) $files[$i] = array();
                     $files[$i][$k] = $v;
                  }
               }

               foreach ($files as $key => $file) {
                  // Move file to the desired folder and save in the Database
                  $file_data['name'] = basename($file[$key]['name']);
                  $file_data['url'] = "https://your-domain.com/images/" . $file_data['name'];
                  $file_data['size'] = $file[$key]['size'];
                  move_uploaded_file($file[$key]['tmp_name'], '/upload/' . $file_data['name']);
                  // INSERT into Database 
               }

               /**
                * for single upload
                * Example: move_uploaded_file($_FILES['eoFileUpload']['tmp_name'], '/upload/' . $file_data['name']);
               */
            }
            ```