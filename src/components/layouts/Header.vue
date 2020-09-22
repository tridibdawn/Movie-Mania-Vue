<template>
<div>
  <b-navbar type="dark" variant="dark" class="px-4">
    <b-navbar-brand to="/" exact>Movie Mania</b-navbar-brand>
    <b-navbar-nav>
      <b-nav-item to="/" exact>Home</b-nav-item>
      <b-nav-item to="/movies" exact>Movies</b-nav-item>
      <b-nav-item to="/about" exact>About</b-nav-item>
    </b-navbar-nav>
  </b-navbar>
  </div>
</template>

<script>
export default {
    name: 'Header'
}
</script>
