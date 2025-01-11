<template>
    <!-- ========== { HEADER }==========  -->
    <header class="fixed top-0 left-0 right-0 z-40">
        <nav class="main-nav">
            <div class="container xl:max-w-6xl mx-auto px-4">
                <div class="lg:flex lg:justify-between">
                    <div class="flex justify-between">
                        <div class="mx-w-10 text-4xl font-bold capitalize text-gray-900 flex items-center">NetBuzz</div>
                        <!-- mobile nav -->
                        <div class="flex flex-row items-center py-4 lg:py-0">
                            <div class="relative text-gray-900 hover:text-black block lg:hidden">
                                <button type="button" class="menu-mobile block py-3 px-6 border-b-2 border-transparent">
                                    <span class="sr-only">Mobile menu</span>
                                    <svg class="open h-8 w-8" xmlns="http://www.w3.org/2000/svg" fill="none"
                                        viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M4 6h16M4 12h16M4 18h16"></path>
                                    </svg>

                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                        class="close bi bi-x-lg h-8 w-8" viewBox="0 0 16 16">
                                        <path fill-rule="evenodd"
                                            d="M13.854 2.146a.5.5 0 0 1 0 .708l-11 11a.5.5 0 0 1-.708-.708l11-11a.5.5 0 0 1 .708 0Z" />
                                        <path fill-rule="evenodd"
                                            d="M2.146 2.146a.5.5 0 0 0 0 .708l11 11a.5.5 0 0 0 .708-.708l-11-11a.5.5 0 0 0-.708 0Z" />
                                    </svg>
                                </button>
                            </div>
                        </div>
                    </div>

                    <div class="flex flex-row">
                        <!-- nav menu -->
                        <ul
                            class="navbar bg-white lg:bg-transparent w-full hidden text-center lg:text-left lg:flex lg:flex-row text-gray-900 text-sm items-center font-bold">
                            <li class="relative hover:text-black">
                                <a class="active block py-3 lg:py-7 px-6 border-b-2 border-transparent"
                                    href="#hero">Home</a>
                            </li>
                            <li class="relative hover:text-black">
                                <a class="block py-3 lg:py-7 px-6 border-b-2 border-transparent" href="#services">What
                                    we do</a>
                            </li>
                            <li class="relative hover:text-black">
                                <a class="block py-3 lg:py-7 px-6 border-b-2 border-transparent" href="#portfolio">Our
                                    works</a>
                            </li>
                            <li class="relative hover:text-black">
                                <a class="block py-3 lg:py-7 px-6 border-b-2 border-transparent" href="#team">Team</a>
                            </li>
                            <li class="relative hover:text-black">
                                <a class="block py-3 lg:py-7 px-6 border-b-2 border-transparent"
                                    href="#contact">Contact</a>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </nav>
    </header><!-- end header -->
</template>

<script setup>
import { onMounted } from 'vue'

// if scroll down
const myScrollspy = function () {
    let scrollpos = document.body.scrollTop || document.documentElement.scrollTop;
    let nav_height = 80;
    let main_nav = document.querySelector(".main-nav");

    // navbar on scroll
    let add_class_on_scroll = function add_class_on_scroll() {
        return main_nav.classList.add("navbar-scrolled")
    };
    let remove_class_on_scroll = function remove_class_on_scroll() {
        return main_nav.classList.remove("navbar-scrolled")
    };

    let navCustom = function navCustom() {
        scrollpos = document.body.scrollTop || document.documentElement.scrollTop;

        if (scrollpos >= nav_height) {
            add_class_on_scroll();
        } else {
            remove_class_on_scroll();
        }
    }

    let navCustomone = function navCustomone() {
        let section = document.querySelectorAll(".section");
        if (section != null) {
            let sections = {};
            let i = 0;

            Array.prototype.forEach.call(section, function (e) {
                sections[e.id] = e.offsetTop;
            });

            window.onscroll = function () {
                let scrollPosition = document.documentElement.scrollTop || document.body.scrollTop;

                for (i in sections) {
                    if (sections[i] <= scrollPosition + nav_height) {
                        document.querySelector('.navbar>li>.active').classList.remove('active');
                        document.querySelector('a[href*=' + i + ']').classList.add('active');
                    }
                }
            }
        }
    }

    // if nav start not in top and not scroll
    window.addEventListener('load', function () {
        document.documentElement.scrollTop = 0;
        document.body.scrollTop = 0;
        navCustom();
        navCustomone();
    });

    // if nav scroll
    window.addEventListener('scroll', function () {
        navCustom();
        navCustomone();
    });
}

// menu mobile
const menu_Mobile = function menu_Mobile() {
    let menu_dropa = document.querySelectorAll(".menu-mobile");
    let menu_menu_x = document.querySelectorAll(".navbar");

    let _loop = function _loop(i) {
        menu_dropa[i].addEventListener("click", function (event) {
            menu_dropa[i].classList.toggle("show");
            menu_menu_x[i].classList.toggle("hidden");

        });
        menu_menu_x[i].addEventListener("click", function (event) {
            menu_dropa[i].classList.toggle("show");
            menu_menu_x[i].classList.toggle("hidden");

        });
    };

    for (let i = 0; i < menu_dropa.length; i++) {
        _loop(i);
    }
};

onMounted(() => {
    myScrollspy();
    menu_Mobile();
})
</script>

<style scoped>
.navbar>li:hover>a:before {
    background-color: var(--primary);
}

/* navslider hover */
.navslider-hover .splide__arrow {
    display: none;
}

.navslider-hover:hover .splide__arrow {
    display: flex;
}

.stroke-primary {
    stroke: var(--primary);
}

.grayscale {
    filter: grayscale(100%);
}

.hover-grayscale-0:hover .grayscale {
    filter: grayscale(0%);
}

.navbar-scrolled {
    background-color: #ffffff;
    border-bottom: var(--gray) 1px solid;
}

.navbar>li>a.active:before {
    background-color: var(--primary);
}

.menu-mobile.show .close {
    display: block;
}

.menu-mobile.show .open,
.menu-mobile .close {
    display: none;
}

.navbar>li>a:before {
    content: '';
    position: absolute;
    left: 50%;
    bottom: .75rem;
    transform: translateX(-50%);
    -webkit-transform: translateX(-50%);
    transform-origin: 50% 50%;
    -webkit-transform-origin: 50% 50%;
    height: 2px;
    width: 1.6rem;
    background-color: transparent;
}

/*Dropdown*/
.dropdown-menu {
    display: none;
}

.dropdown-menu.show {
    display: block;
}

@media (min-width: 1024px) {
    .navbar .dropdown-menu.show {
        display: none;
    }

    .navbar .dropdown:hover>.dropdown-menu,
    .navbar .dropdown:hover>.dropdown-menu.show {
        display: block;
    }

    .navbar .dropdown-menu>li:hover>.dropdown-menu,
    .navbar .dropdown-menu>li:hover>.dropdown-menu.show {
        display: block;
    }
}

/*Caret*/
.dropdown>a:after,
.subdropdown>a:after {
    content: "";
    display: inline-block;
    width: .8rem;
    height: .8rem;
    background-repeat: no-repeat;
    background-size: .8rem .8rem;
    vertical-align: middle;
    margin-left: .4rem;
    margin-top: .2rem;
}

.dropdown>a:after {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3e%3cpolyline points='112 184 256 328 400 184' fill='none' stroke='%23555555' stroke-linecap='round' stroke-linejoin='round' stroke-width='48px'/%3e%3c/svg%3e");
}

.navbar .dropdown>a:after {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3e%3cpolyline points='112 184 256 328 400 184' fill='none' stroke='%23f9f9f9' stroke-linecap='round' stroke-linejoin='round' stroke-width='48px'/%3e%3c/svg%3e");
}

.subdropdown>a:after {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3e%3cpolyline points='112 184 256 328 400 184' fill='none' stroke='%23555555' stroke-linecap='round' stroke-linejoin='round' stroke-width='48px'/%3e%3c/svg%3e");
}

.navbar .subdropdown>a:after {
    transform: rotate(-90deg);
}
</style>
