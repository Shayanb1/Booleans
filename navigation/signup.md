---
layout: page 
title: Sign Up
permalink: /signup
search_exclude: true
---

{% include nav/homejava.html%}

<style>
.login-container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap; /* allows the cards to wrap onto the next line if the screen is too small */
}




.signup-card {
    margin: auto;
    margin-top: 0; /* remove the top margin */
    width: 45%;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    margin-bottom: 20px;
    overflow-x: auto; /* Enable horizontal scrolling */
}

.signup-card h1 {
    margin-bottom: 20px;
}
</style>

<div id="login-container">
<div class="signup-card">
        <h1 id="signupTitle">Sign Up</h1>
        <form id="signupForm" onsubmit="signup(); return false;">
            <p>
                <label>
                    Name:
                    <input type="text" name="name" id="name" required>
                </label>
            </p>
            <p>
                <label>
                    Github Id:
                    <input type="text" name="signupUid" id="signupUid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="signupPassword" id="signupPassword" required>
                </label>
            </p>
            <p>
                <label>
                    <input type="checkbox" name="kasmNeeded" id="kasmNeeded">
                    Kasm Server Needed
                </label>
            </p>
            <p>
                <button type="submit">Sign Up</button>
            </p>
            <p id="signupMessage" style="color: green;"></p>
        </form>
    </div>
</div>
<div class="output-box" id="outputBox">HERE</div>

<!--
<script type="module">
    import { login, pythonURI, fetchOptions } from '{{site.baseurl}}/assets/js/api/config.js';

    // Function to handle signup
    window.signup = function() {
    const signupButton = document.querySelector(".signup-card button");

    // Disable the button and change its color
    signupButton.disabled = true;
    signupButton.style.backgroundColor = '#d3d3d3'; // Light gray to indicate disabled state

    const signupOptions = {
        URL: `${pythonURI}/api/user`,
        method: "POST",
        cache: "no-cache",
        body: {
            name: document.getElementById("name").value,
            uid: document.getElementById("signupUid").value,
            password: document.getElementById("signupPassword").value,
            kasm_server_needed: document.getElementById("kasmNeeded").value,
        }
    };

    fetch(signupOptions.URL, {
        method: signupOptions.method,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(signupOptions.body)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error(`Signup failed: ${response.status}`);
        }
        return response.json();
    })
    .then(data => {
        document.getElementById("signupMessage").textContent = "Signup successful!";
        // Optionally redirect to login page or handle as needed
        // window.location.href = '{{site.baseurl}}/profile';
    })
    .catch(error => {
        console.error("Signup Error:", error);
        document.getElementById("signupMessage").textContent = `Signup Error: ${error.message}`;
        // Re-enable the button if there is an error
        signupButton.disabled = false;
        signupButton.style.backgroundColor = ''; // Reset to default color
    });
}


    // Function to fetch and display Python data
    function pythonDatabase() {
        const URL = `${pythonURI}/api/id`;

        fetch(URL, fetchOptions)
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Flask server response: ${response.status}`);
                }
                return response.json();
            })
            .then(data => {
                window.location.href = '{{site.baseurl}}/profile';
            })
            .catch(error => {
                console.error("Python Database Error:", error);
                const errorMsg = `Python Database Error: ${error.message}`;
            });
    }

    // Call relevant database functions on the page load
    window.onload = function() {
         pythonDatabase();
    };
</script>
-->


<script type="module">
  import { javaURI, pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';


  

window.signup = function(){
    // clones and replaces method
    const signupOptions = {
        URL: `${javaURI}/api/person/create`,
        method: "POST",
        cache: "no-cache",
        headers: (new Headers({"Content-Type":"application/json"})),
        body: JSON.stringify({
                uid:   document.getElementById("signupUid").value,
                email: document.getElementById("signupUid").value + "@gmail.com",
                dob: "11-01-2024",
                name: document.getElementById("name").value,
                password: document.getElementById("signupPassword").value,
                kasmServerNeeded: document.getElementById("kasmNeeded").checked,
            
        }),
    };
  }

  // Something went wrong with actions or responses
  function error(err) {
    // log as Error in console
    console.error(err);
    // append error to resultContainer
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    document.getElementById("login-container").appendChild(tr);
  }

</script>