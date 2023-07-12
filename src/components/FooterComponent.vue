<template>
    <footer :class="{dark: darkMode}" class="footer">
      <div class="container">
        <div class="footer-info">
          <h4>À propos de l'application</h4>
          <p>Générateur d'images provenant de l'API sp-clothes</p>
          <p>{{ appDescription }}</p>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; {{ currentYear }} Mon Application</p>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    props: {
      darkMode: {
        type: Boolean,
        required: true,
      }
    },
    data() {
      return {
        isDarkTheme: this.$parent.darkMode,
        currentYear: new Date().getFullYear(),
        appDescription: "Cette application génère des images à partir de l'API sp-clothes en utilisant diverses fonctionnalités et données fournies par l'API. Elle permet aux utilisateurs de créer des images personnalisées à partir des données de l'API.",
      };
    },
  };
  </script>
  
  <style scoped>
  .footer {
    background-color: #f5f5f5;
    padding: 20px 0;
    text-align: center;
  }

  .dark {
    background-color: #2c3e50;
    color: #fff;
  }
  
  .container {
    max-width: 960px;
    margin: 0 auto;
  }
  
  .footer-info,
  .footer-links,
  .footer-social {
    margin-bottom: 20px;
  }
  
  h4 {
    margin: 0;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }
  
  ul li {
    margin-bottom: 10px;
  }
  
  ul li a {
    color: #333;
    text-decoration: none;
  }
  
  .footer-social ul li {
    display: inline-block;
    margin-right: 10px;
  }
  
  .footer-social ul li a {
    color: #333;
    font-size: 20px;
  }
  
  .footer-bottom {
    margin-top: 20px;
  }
  
  p {
    margin: 0;
  }
  </style>
  