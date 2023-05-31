<template>
  <main font-sans p="x-4" text="center gray-700 dark:gray-200">
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
  </main>
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
  z-index: 100;
  height: 100px;
}

.main-content {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  height: calc(100vh - 100px - 80px); /* set the height to 100% */
  overflow-y: auto; /* add a scrollbar to the main content if it overflows */
  padding: 20px; /* add padding to the main content for better readability */
}

.footer-fixed {
  position: sticky;
  bottom: 0;
  z-index: 100;
  height: 80px;
}
</style>
