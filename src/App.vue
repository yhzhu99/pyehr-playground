<template>
  <div font-sans p="x-4" text="center gray-700 dark:gray-200">
    <container class="flex-container">
      <header class="header-fixed">
        <TheHeader />
      </header>
      <main class="main-content">
        <RouterView />
      </main>
      <footer class="footer-fixed">
        <TheFooter />
      </footer>
    </container>
  </div>
</template>

<style scoped>
.flex-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.header-fixed {
  position: sticky;
  top: 0;
  z-index: 100000;
}

.main-content {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%; /* set the height to 100% */
  overflow-y: auto; /* add a scrollbar to the main content if it overflows */
}

.footer-fixed {
  position: sticky;
  bottom: 0;
  z-index: 100000;
}
</style>
