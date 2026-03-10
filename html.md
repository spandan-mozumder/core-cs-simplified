# 🏷️ HTML — Interview Questions & Answers

> Top HTML interview questions with answers and code examples.
> Source: [Intellipaat — HTML Interview Questions](https://intellipaat.com/blog/interview-question/html-interview-questions/)

---

### Q1. What is HTML?

**HTML** (HyperText Markup Language) is the standard markup language for creating web pages. It defines the structure and content of a webpage using tags.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

---

### Q2. What are HTML Tags, Elements, and Attributes?

- **Tag**: `<p>`, `<div>`, `<a>` — markup syntax
- **Element**: `<p>Content</p>` — opening tag + content + closing tag
- **Attribute**: Provides extra info → `<a href="url" target="_blank">`

---

### Q3. `<div>` vs `<span>`

| `<div>`                  | `<span>`                |
| ------------------------ | ----------------------- |
| Block-level element      | Inline element          |
| Takes full width         | Takes only needed width |
| Used for layout sections | Used for styling text   |

```html
<div style="background: lightblue; padding: 10px;">
  This is a block container.
  <span style="color: red;">This is inline text.</span>
</div>
```

---

### Q4. Semantic Tags in HTML5

```html
<!-- Non-semantic (no meaning) -->
<div class="header">...</div>

<!-- Semantic (meaningful) -->
<header>Site header</header>
<nav>Navigation links</nav>
<main>
  <article>
    <section>Content section</section>
  </article>
  <aside>Sidebar</aside>
</main>
<footer>Site footer</footer>
```

**Why semantic?** SEO, accessibility (screen readers), code readability.

---

### Q5. Block vs Inline vs Inline-Block

| Type             | Width         | Stacking                          | Example                     |
| ---------------- | ------------- | --------------------------------- | --------------------------- |
| **Block**        | Full width    | Vertical                          | `<div>`, `<p>`, `<h1>`      |
| **Inline**       | Content width | Horizontal                        | `<span>`, `<a>`, `<strong>` |
| **Inline-block** | Content width | Horizontal (can set width/height) | `<img>`, custom buttons     |

---

### Q6. HTML Forms

```html
<form action="/submit" method="POST">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required placeholder="John" />

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required />

  <label for="password">Password:</label>
  <input type="password" id="password" name="password" minlength="8" />

  <label for="age">Age:</label>
  <input type="number" id="age" name="age" min="18" max="100" />

  <label for="gender">Gender:</label>
  <select id="gender" name="gender">
    <option value="male">Male</option>
    <option value="female">Female</option>
  </select>

  <label>
    <input type="checkbox" name="terms" required /> I agree to terms
  </label>

  <button type="submit">Submit</button>
  <button type="reset">Reset</button>
</form>
```

---

### Q7. HTML Tables

```html
<table border="1">
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>25</td>
      <td>NYC</td>
    </tr>
    <tr>
      <td colspan="2">Bob (spans 2 cols)</td>
      <td>LA</td>
    </tr>
  </tbody>
</table>
```

---

### Q8. id vs class

| Feature      | `id`                    | `class`                    |
| ------------ | ----------------------- | -------------------------- |
| Uniqueness   | Must be unique per page | Can be reused              |
| CSS selector | `#myId`                 | `.myClass`                 |
| JS access    | `getElementById()`      | `getElementsByClassName()` |
| Specificity  | Higher                  | Lower                      |

---

### Q9. HTML5 New Input Types

```html
<input type="date" />
<input type="time" />
<input type="datetime-local" />
<input type="color" />
<input type="range" min="0" max="100" />
<input type="url" />
<input type="tel" />
<input type="search" />
```

---

### Q10. localStorage vs sessionStorage

```html
<script>
  // localStorage — persists even after browser closes
  localStorage.setItem("username", "Alice");
  console.log(localStorage.getItem("username")); // "Alice"
  localStorage.removeItem("username");

  // sessionStorage — cleared when tab/browser closes
  sessionStorage.setItem("token", "abc123");
  console.log(sessionStorage.getItem("token"));
</script>
```

---

### Q11. `<meta>` Tags

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="A great website" />
  <meta name="keywords" content="HTML, CSS, JavaScript" />
  <meta name="author" content="John Doe" />
  <meta http-equiv="refresh" content="30" />
  <!-- Auto-refresh every 30 sec -->
</head>
```

---

### Q12. Audio & Video in HTML5

```html
<video width="640" height="360" controls autoplay muted>
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  Your browser does not support the video tag.
</video>

<audio controls>
  <source src="audio.mp3" type="audio/mpeg" />
  <source src="audio.ogg" type="audio/ogg" />
</audio>
```

---

### Q13. `<iframe>` — Embedding External Content

```html
<iframe
  src="https://www.example.com"
  width="600"
  height="400"
  title="Example Site"
  sandbox="allow-scripts"
  loading="lazy"
>
</iframe>
```

---

### Q14. HTML Entities

```html
&lt; → < &gt; → > &amp; → & &nbsp; → non-breaking space &copy; → © &reg; → ®
&quot; → "
```

---

### Q15. HTML5 Canvas

```html
<canvas id="myCanvas" width="300" height="200"></canvas>
<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");

  ctx.fillStyle = "#3498db";
  ctx.fillRect(20, 20, 150, 100);

  ctx.beginPath();
  ctx.arc(250, 100, 50, 0, Math.PI * 2);
  ctx.fillStyle = "#e74c3c";
  ctx.fill();

  ctx.font = "20px Arial";
  ctx.fillStyle = "#000";
  ctx.fillText("Hello Canvas!", 20, 180);
</script>
```

---

### Q16. Void Elements

Self-closing tags that don't have content:

```html
<br />
<!-- Line break -->
<hr />
<!-- Horizontal rule -->
<img />
<!-- Image -->
<input />
<!-- Input field -->
<meta />
<!-- Metadata -->
<link />
<!-- External resource -->
```

---

### Q17. SVG in HTML

```html
<svg width="200" height="200">
  <circle
    cx="100"
    cy="100"
    r="80"
    fill="#3498db"
    stroke="#2c3e50"
    stroke-width="3"
  />
  <text x="100" y="110" text-anchor="middle" fill="white" font-size="20">
    SVG
  </text>
</svg>
```

| SVG                     | Canvas                       |
| ----------------------- | ---------------------------- |
| Vector (scalable)       | Raster (pixel-based)         |
| DOM elements            | Drawn with JS                |
| Better for logos, icons | Better for games, animations |

---

### Q18. Data Attributes

```html
<div id="user" data-user-id="123" data-role="admin">Alice</div>
<script>
  const el = document.getElementById("user");
  console.log(el.dataset.userId); // "123"
  console.log(el.dataset.role); // "admin"
</script>
```

---

### Q19. Geolocation API

```html
<script>
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      (pos) => {
        console.log(`Lat: ${pos.coords.latitude}`);
        console.log(`Lng: ${pos.coords.longitude}`);
      },
      (err) => console.error(err.message),
    );
  }
</script>
```

---

### Q20. `readonly` vs `disabled`

| `readonly`                       | `disabled`                 |
| -------------------------------- | -------------------------- |
| User can't edit, CAN select/copy | User can't interact at all |
| Value IS submitted with form     | Value NOT submitted        |
| Focusable                        | Not focusable              |

```html
<input type="text" value="Read Only" readonly />
<input type="text" value="Disabled" disabled />
```

---
