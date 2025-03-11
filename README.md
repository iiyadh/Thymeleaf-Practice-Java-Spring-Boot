# Spring Boot + Thymeleaf Practice Project

This project serves as hands-on practice for understanding the integration and workflow of **Thymeleaf** with **Spring Boot 3**. It provides a simple example of building a dynamic web page using server-side rendering with Thymeleaf templates.

## ✨ Features

- Learn how to pass data from a Spring Boot controller to a Thymeleaf view.
- Dynamically render content using Thymeleaf conditionals and fragments.
- Practice building a real-world project layout with header, footer, and reusable components.
- Demonstrate multilingual support using conditional logic (`fr` and `en`).

## 📁 Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com.isett.backend/
│   │       └── HomeController.java
│   └── resources/
│       ├── templates/
│       │   ├── index.html
│       │   └── fragments/
│       │       └── details.html
│       ├── static/
│       │   ├── css/
│       │   │   └── styles.css
│       │   └── img/
│       │       ├── iset.JPG
│       │       └── Spring.png
```

## 🧠 How It Works

### Controller (Java)
The `HomeController` handles GET requests to `/`. It passes a list of learning features to the view and conditionally includes additional details based on the `showDetails` query parameter.

```java
@GetMapping("/")
public String home(@RequestParam(name = "showDetails", required = false) boolean showDetails, Model model) {
    model.addAttribute("features", Arrays.asList(
        "Travailler sur des projets avec un Tuteur",
        "Avoir du retour sur expériences sur votre travail",
        "Apprendre les meilleurs pratiques du Software Design"
    ));
    model.addAttribute("showDetails", showDetails);
    return "index";
}
```

### Thymeleaf View (HTML)
The main page `index.html` includes a dynamic section rendered only when `showDetails` is `true`. This section is pulled from a fragment `details.html`, supporting multilingual display based on a passed language.

```html
<div th:if="${showDetails}">
    <div th:replace="~{fragments/details.html :: content('en')}" />
</div>
```

### Fragment `details.html`
This file contains the list of features, displayed based on the selected language:

```html
<h3 th:if="${lang == 'fr'}"> Ce que vous allez apprendre </h3>
<h3 th:if="${lang == 'en'}"> What you will learn </h3>
<ul th:each="item: ${features}">
    <li th:text="${item}" />
</ul>
```

## 🏁 Getting Started

To run this project:
1. Clone the repository.
2. Open it in your favorite IDE.
3. Make sure you have Java and Maven installed.
4. Run the application using your IDE or `mvn spring-boot:run`.

Visit [http://localhost:8080](http://localhost:8080) and add `?showDetails=true` to the URL to see extra content.

---

© ISET Tozeur
