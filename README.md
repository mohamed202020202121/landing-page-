/*create some parent ul(fragment) element outside of the loop
we could append all new li (listItem) elements to this parent ul
this not from l5 performance/2
*/
// I use .createDocumentFragment for high performance and to avoid repain & reflow
const fragment = document.createDocumentFragment();

/*
*I try to access to tag (section) by the query selector method
*I studied this code in ( L2 . the Document object model / 7 . more ways to access element)
* I can use also to access to this tag (section) by this code (document.getElementsByTagName())
*I studied this code in ( L2 . the Document object model / 5 . Select Page Elements By Class Or Tag)
*/
const sections = document.querySelectorAll('section');
/*
*create navbar (ul)
*access to ul by using its id (('navbar__list'))
*I Select this element by this code  document.getElementById('navbar__list')
*I studied this code at( L2 . the Document object model / 4 .Select Page Element By ID)
* I also can select by this code document.querySelector('#navbar__list');
* I studied this code in ( L2 . the Document object model / 7 . more ways to access element)
*/
const navbar = document.getElementById('navbar__list');
/*
* navbar will return in array [];
* so I will use forEach() loop to manipulate each element in the array with an inline function expression
* I studied this code in ( L6 . Arrays / 8 . The forEach Loop);
*/

sections.forEach(function(section){
  //not found through the course
  //did some search in this web developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute
      name = section.getAttribute('data-nav');
      link = section.getAttribute('id');
      listItem = document.createElement('li');
      listItem.innerHTML= `<a class='menu__link' href='#${link}''>${name}</a>`;
      section.scrollIntoView({behavior: "smooth"});

 fragment.appendChild(listItem);
});
navbar.appendChild(fragment);
function sectionInViewPort(elem){
  let sectionPos = elem.getBoundingClientRect();
  return(sectionPos.top>=0);
}
function toggleActiveClass(){
  for (section of sections){
    if (sectionInViewPort(section)){
      if (!section.classList.contains("your-active-class")){
      section.classList.add("your-active-class");
      }else {  section.classList.remove("your-active-class");}
    }
  }
}
document.addEventListener('scroll', toggleActiveClass);
