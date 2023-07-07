<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li><router-link to="/">Cuaca</router-link></li>
          <li><router-link to="/location">Lokasi</router-link></li>
          <li><router-link to="/stopwatch">Penghitung Detik</router-link></li>
          <li><router-link to="/TicTacToeWidget">Tic Tac Toe</router-link></li>
          <li><router-link to="/photo">Foto</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>

#app {
  text-align: center;
  
  
}


header {
  background: #697184;
  padding: 22px;
  border-radius: 3px;
  box-shadow: 1px 2px 2px ;
  margin-bottom: 12px;
  
}

nav ul {
  list-style:circle;
  margin: 0;
  padding: 0;
  
  
}

nav li {
  display:inline-block;
  margin-right: 5px;
  margin-bottom: 3px;
  background-color: #f0efeb;
  padding: 10px;
  border-radius: 3px;
  box-shadow: #4690b3 2px 2px;
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;

}

nav a {
  color: #000000;
  text-decoration: none;
  padding: 65px;
  
}

nav a:hover {
  text-decoration: underline;
  color: #fc40d3;
  
  
  

}
</style>
