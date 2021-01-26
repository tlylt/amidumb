<header>
  <navbar type="dark">
    <a slot="brand" href="{{baseUrl}}/index.html" title="Home" class="navbar-brand">L</a>
    <li slot="right">
      <form class="navbar-form">
        <searchbar :data="searchData" placeholder="Search" :on-hit="searchCallback" menu-align-right></searchbar>
      </form>
    </li>
  </navbar>
</header>
