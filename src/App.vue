<template>
    <nav class="navbar navbar-expand-lg bg-dark" id="ftco-navbar" >
       <div class="container">
           <a class="navbar-brand text-white" >PRACTICA 1</a>
           <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#ftco-nav" aria-controls="ftco-nav" aria-expanded="false" aria-label="Toggle navigation">
               <span class="fa fa-bars text-primary"></span> 
           </button>
           <div class="collapse navbar-collapse" id="ftco-nav">
               <ul class="navbar-nav ms-auto"> 
                   <li class="nav-item ">
                       <router-link to="/" class="nav-link text-white"><b>Inicio</b></router-link>
                   </li>
                   <li class="nav-item">
                       <router-link to="/integrantes" class="nav-link text-white"><b>Integrantes</b></router-link>
                   </li>
                   <li class="nav-item">
                       <router-link to="/crud" class="nav-link text-white"><b>CRUD</b></router-link>
                   </li>
   
               </ul>
           </div>
       </div>
   </nav>
   
    
      <router-view/>
    </template>
    
    
    <style lang="scss">
    @import "@/assets/style.css";
    .nav-link {
     transition: color 0.3s ease;
   }
   
   .nav-link:hover {
     color: #007bff !important; 
   }
    </style>
    