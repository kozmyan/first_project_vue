<template>
    <header>
        <div class="header__container">
            <div 
            class="menu__icon"
            @click="burgerMenu"
            >
                <span></span>
            </div>
            <nav class="menu__body">
                <ul class="menu__list">
                    <li class="menu__link">Обо мне</li>
                    <li class="menu__link">Резюме</li>
                    <li class="menu__link">Портфолио</li>
                </ul>
            </nav>
        </div>
    </header>
</template>
  
  
  
<script>
  
  export default {
     
    data() {
      return {
          visibleMenu: false,
      }
    },
    methods: {
       burgerMenu(){
        
       },

//        const iconMenu = document.querySelector('.menu__icon');
// if(iconMenu){
//  const menuBody = document.querySelector('.menu__body');
//  iconMenu.addEventListener('click', function(e){
//     iconMenu.classList.toggle('_active');
//     menuBody.classList.toggle('_active');
//  });
}

}

   

  
  </script>
  
  
  
  
<style scoped>
header {
    width: 100%;
    height: 5em;
    background: rgb(10, 7, 51);
    color: white;
    display: flex;
    align-items: center;
    
}

.menu__icon {
    display: none;
}

.menu__list {
    display: flex;
}

.menu__link {
    font-size: 1em;
    color: #FFFFFF;
    margin-left: 1.5em;
    cursor: pointer;
}

.menu__link:hover {
    color: #e5ff00;
    transition: 0.5s;
    cursor: pointer;
}











@media (max-width: 1150px) {
    .header__container {
        padding: 0px 70px;
    }
}

@media (max-width: 991.98px) {
    .header__container {
        padding: 0px 70px;
    }

}

@media (max-width: 768px) {
    .header__container {
        padding: 0px 70px;
    }

    .menu__icon {
        z-index: 5;
        display: block;
        position: relative;
        width: 40px;
        height: 25px;
        cursor: pointer;
        transition: all 0.3s ease 0s;
    }

    .menu__icon::before,
    .menu__icon::after,
    .menu__icon span {
        left: 0;
        position: absolute;
        height: 5px;
        width: 100%;
        background-color: #FFFFFF;
        border-radius: 15px;
        transition: all 0.3s ease 0s;
    }

    .menu__icon::before,
    .menu__icon::after {
        content: "";
    }

    .menu__icon::before {
        top: 0;
    }

    .menu__icon::after {
        bottom: 0;
    }

    .menu__icon span {
        top: 50%;
        transform: scale(1) translate(0px, -50%)
    }

    .menu__icon._active span {
        transform: scale(0) translate(0px, -50%)
    }

    .menu__icon._active::before {
        top: 45%;
        transform: rotate(45deg) translate(0px, -50%)
    }

    .menu__icon._active::after {
        bottom: 45%;
        transform: rotate(-45deg) translate(0px, 50%)
    }

    .menu__list {
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    .menu__body {
        position: fixed;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        transition: left 0.3s ease 0s;
        background: #000;
        opacity: 0.95;
        padding-top: 120px;

    }

    .menu__body._active {
        left: 0;
    }

    
    
}

</style>