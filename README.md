# Github Followers


**How does my project look**


![github followers](https://github.com/kaplanh/github-followers/assets/101884444/53c26f47-ffaf-45f0-bb7d-733eb06fe7a3)

[Live link!](https://kaplanh.github.io/github-followers/)


 **What's used in this app ?** | **How to run ?** | **Author** |
|----------|---------|------------
|Api-Server | Once you clone the project|[Take a look at my portfolio](https://kaplanh.github.io/Portfolio_with_CssFlex/)|
|Html| open index.html with Go Live in vs cod|[Visit me on Linkedin](https://www.linkedin.com/in/kaplan-h/)|
|Css||   
|Javascript |  |
|Bootstrap ||   

**What is this project about ?**
- In this project user can get any current country detail from certain api-server and can find a link which takes the user google map.



## Project Skeleton 

```
Synchronous-Asynchronous-Programming(folder)
|
|----readme.md                        
|----index.html
|----img (folder)
|----style.css
|----1-intro.js
|----2-promise.js
|----3-fetchAPI.js
|----4-async-await.js
```

### At the end of the project, the following topics are to be covered;

- API's
  - [Github followers API](https://api.github.com/users)
  - [newsAPI](https://newsapi.org/)
- HTML
- CSS
 - Nested CSS
     ~~~css
          .card {
              & img {
                  transition: 0.5s;
              }
          
              & img:hover {
                  rotate: 10deg;
                  scale: 1.02;
              }
              & .btn {
                  transition: scale 0.2s;
              }
              & .btn:hover {
                  scale: 1.03;
              }
          }
     ~~~
  
  - JS
     - senkron programing
       ```
       console.log("Hello")
       alert("Blocked") //? Blocking
       console.time("gecikme")
       delay(4000) //? blocking code - senkron
       console.timeEnd("gecikme")
       console.log("hi")
       ```
      - Asenkron (setTimeout()) programing
          ```
           setTimeout(() => {
          console.log("I am fine")
          console.timeEnd("timer")
          }, 1000)
          
          setTimeout(() => {
             console.log("Whats up?")
              console.timeEnd("timer")
           }, 1000)
          
           console.log("start")
           console.time("timer")
             ```
        -  Asenkron (setInterval, clearInterval) programing
             ```
            /? setInterval periyodik zaman araligi oluşturmak icin kullanilabilir.
            //? clearInterval yardımıyla surekli devam interval pasif hale getirilir.
            let count = 0
            const sec1 = setInterval(() => {
              console.log(++count)
              if (count > 9) {
                clearInterval(sec1)
               }
            }, 1000)
              ```
       - Callback Hell (nested ve birbirine bagli callback'ler)
   
              ```
                  setTimeout(() => {
                  console.log("john:Hi");
                  setTimeout(() => {
                      console.log("Sarah: Hello");
                      setTimeout(() => {
                          console.log("John: How Are you?");
                          setTimeout(() => {
                              console.log("Sarah:Fine and you?");
                          }, 1000);
                      }, 1000);
                  }, 1000);
              }, 1000);
              ```
       - Promise()
         
             ```
                   const networkReq = new Promise((resolve, reject) => {
                      const data = { a: 1, b: 2 };
                      const success = Math.floor(Math.random() * 5); //? (0,1,2,3,4)
                      if (success) {
                          console.log("Data fetched");
                          resolve(data);
                      } else {
                          reject("Ohh no there is network error");
                      }
                  });              
              networkReq
                  .then((response) => console.log(response))
                  .then(() => console.log("2. then"))
                  .catch((err) => document.write(err))
                  .finally(() => console.log("Her zaman calisir"));
              ```
      - fetch API
              ```   

                  let veri = "";
                   fetch("https://api.github.com/users")
                     .then((res) => {
                         //! Error handling
                         if (!res.ok) {
                             throw new Error("Something went wrong", res.status);
                             // console.log("Something went wrong")
                         } else {
                             return res.json();
                         }
                     })
                     .then((data) => {
                         // veri = data
                         // console.log(veri)
                         showUsers(data);
                     })
                     .catch((err) => {
                         console.log(err);
                         const usersDiv = document.getElementById("users");
                         usersDiv.innerHTML = `<h2 class="text-warning">${err}</h2>`;
                     });
                 
                 // console.log(veri)
                 
                 const showUsers = (users) => {
                     console.log(users);
                     const usersDiv = document.getElementById("users");
                 
                     users.forEach((user) => {
                         // console.log(user.login)
                         usersDiv.innerHTML += `
                          <div class="card col" style="width: 15rem;">
                             <img src="${user.avatar_url}" class="card-img-top img-thumbnail" alt="...">
                 
                            <div class="card-body">
                 
                             <h5 class="card-title">${user.login}</h5>
                             <p class="card-text">${user.type + ' ' + user.id}</p>
                             <a href="${user.html_url}" class="btn btn-primary">Go somewhere</a>
                 
                            </div>
                 
                        </div>
                     `;
                     });
                 };
               ```
        
       - async-await
           ```
            const getNews = async () => {
                     const API_KEY = "2108f1dba8114b89b4a326fc6f71a5a8";
                     const URL = `https://newsapi.org/v2/top-headlines?country=us&apiKey=${API_KEY}`;
                     try {
                         const res = await fetch(URL);
                         // console.log(res);
                         //?Error handling
                         if (!res.ok) {
                             throw new Error("News can not be fetched");
                         }
                         const data = await res.json();
                         renderNews(data.articles);
                     } catch (err) {
                         // console.log(error);
                         renderError(err);
                     }
                   };
                   const renderNews = (news) => {
                       const newsDiv = document.getElementById("news");

                      news.map((item) => {
                          const { title, content, url, urlToImage } = item; //? destructure
                          newsDiv.innerHTML += `
                      <div class="col-sm-6 col-md-4 col-lg-3">
                          <div class="card">
                              <img src="${urlToImage}" class="card-img-top img-thumbnail" alt="...">
                              <div class="card-body">
                                  <h5 class="card-title">${title}</h5>
                                  <p class="card-text">${content}</p>
                                  <a href="${url}" target="_blank" class="btn btn-danger">Go Detail</a>
                              </div>
                          </div>
                      </div>
           
                               `;
                               });
                           };
                   const renderError = (err) => {
                       const newsDiv = document.getElementById("news");
                       newsDiv.innerHTML = `
                       <h3>${err}</h3>
                       <img src="./img/404.png" alt="404" />
                     `;
                   };
                   
                   window.addEventListener("load", () => {
                       getNews();
                   });```
      
  
    - DOM Manipulations
      - innerHTML
      - innerText
      - textContent
     
    - DOM Selectors
    
    - Events
        - click
        - load
 
 
  
    - Array Methods
    - forEach() &  map()

     ```
             const showUsers = (users) => {
              console.log(users);
              const usersDiv = document.getElementById("users");
          
              users.forEach((user) => {
                  // console.log(user.login)
                  usersDiv.innerHTML += `
                   <div class="card col" style="width: 15rem;">
                      <img src="${user.avatar_url}" class="card-img-top img-thumbnail" alt="...">
          
                     <div class="card-body">
          
                      <h5 class="card-title">${user.login}</h5>
                      <p class="card-text">${user.type + ' ' + user.id}</p>
                      <a href="${user.html_url}" class="btn btn-primary">Go somewhere</a>
          
                     </div>
          
                 </div>
              `;
              });
          };
       ```





     ```
            const renderNews = (news) => {
            const newsDiv = document.getElementById("news");
        
            news.map((item) => {
                const { title, content, url, urlToImage } = item; //? destructure
                newsDiv.innerHTML += `
            <div class="col-sm-6 col-md-4 col-lg-3">
                <div class="card">
                    <img src="${urlToImage}" class="card-img-top img-thumbnail" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">${title}</h5>
                        <p class="card-text">${content}</p>
                        <a href="${url}" target="_blank" class="btn btn-danger">Go Detail</a>
                    </div>
                </div>
            </div>
           
            `;
            });
        };
            });
    ```
 


## Feedback and Collaboration
I value your feedback and suggestions. If you have any comments, questions, or ideas for improvement regarding this project or any of my other projects, please don't hesitate to reach out.
I'm always open to collaboration and welcome the opportunity to work on exciting projects together.
Thank you for visiting my project. I hope you have a wonderful experience exploring it, and I look forward to connecting with you soon!



<p align="center"> ⌛<strong> Happy Coding </strong> ✍ </p>





