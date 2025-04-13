<script lang="ts">
  import { getCurrentWindow } from "@tauri-apps/api/window";
  import "@fortawesome/fontawesome-free/css/all.min.css";

  const appWindow = getCurrentWindow();
  let drawerOpen = $state(false);

  function toggleDrawer() {
    drawerOpen = !drawerOpen;
  }

  function minimize() {
    appWindow.minimize();
  }

  function toggleMaximize() {
    appWindow.toggleMaximize();
  }

  function closeWindow() {
    appWindow.close();
  }
</script>

<input
  id="app-drawer"
  type="checkbox"
  class="drawer-toggle"
  bind:checked={drawerOpen}
/>

<div class="drawer-content flex flex-col">
  <!-- Titlebar -->
  <div
    class="bg-gradient-to-r from-green-950/15 via-emerald-900/10 to-green-950/15 backdrop-blur-xl h-8 fixed top-0 left-0 right-0 flex items-center justify-between z-50 px-2 border-b border-green-800/10"
    data-tauri-drag-region
  >
    <!-- Left section -->
    <div class="flex items-center gap-2" data-tauri-drag-region>
      <!-- Back button -->
      <button
        class="btn btn-ghost btn-sm h-8 w-12 -ml-2 rounded-none"
        aria-label="Go Back"
      >
        <i class="fas fa-arrow-left"></i>
      </button>
      <div class="w-5 h-5">
        <img src="/setscript.png" alt="SetScript icon" class="w-8" />
      </div>
      <div class="text-sm font-medium" data-tauri-drag-region>SetScript</div>
    </div>

    <!-- Middle -->
    <div class="flex-grow" data-tauri-drag-region></div>

    <!-- Right section (add back button here) -->
    <div class="flex justify-end w-full -mr-2">
      <!-- Sidebar toggle -->
      <label
        for="app-drawer"
        class="btn btn-ghost btn-sm h-8 w-12 rounded-none drawer-button hover:bg-green-800/10"
      >
        <i class="fas fa-bars text-sm"></i>
      </label>

      <!-- Window controls -->
      <div class="flex">
        <button
          class="btn btn-ghost btn-sm h-8 w-12 rounded-none hover:bg-green-800/10"
          onclick={minimize}
          aria-label="Minimize window"
        >
          <i class="fas fa-window-minimize"></i>
        </button>
        <button
          class="btn btn-ghost h-8 w-12 rounded-none hover:bg-green-800/10"
          onclick={toggleMaximize}
          aria-label="Maximize window"
        >
          <i class="far fa-square"></i>
        </button>
        <button
          class="btn btn-ghost btn-error h-8 w-12 rounded-none hover:text-red-500"
          onclick={closeWindow}
          aria-label="Close window"
        >
          <i class="fas fa-times text-[16px]"></i>
        </button>
      </div>
    </div>
  </div>
</div>

<!-- Drawer sidebar -->
<div class="drawer-side pt-8 z-12">
  <label
    for="app-drawer"
    aria-label="close sidebar"
    class="drawer-overlay fixed top-8 left-0 right-0 bottom-0"
  ></label>

  <div
    class="p-3 w-64 min-h-full bg-gradient-to-r from-neutral-950/30 to-green-950/5 backdrop-blur-2xl text-base-content flex flex-col"
  >
    <div class="flex justify-center w-full">
      <img src="/setscript.png" alt="SetScript icon" class="w-24 my-4" />
    </div>

    <div class="text-xl font-semibold text-center mb-4">SetScript Desktop</div>
    <ul class="menu text-base-content text-xl w-full">
      <li>
        <a href="/" class="flex items-center gap-2">
          <i class="fas fa-cog"></i> Ayarlar
        </a>
      </li>
      <li>
        <a href="/" class="flex items-center gap-2">
          <i class="fas fa-info-circle"></i> Hakkımızda
        </a>
      </li>
    </ul>
    <div class="text-xs font-light text-center mt-auto mb-10">
      Setscript Desktop uygulaması, <br />
      <a
        href="https://github.com/setscript/setscript-desktop-tauri"
        target="_blank"
        class="underline">gönüllüler</a
      > tarafından ❤️ ile yapıldı.
    </div>
  </div>
</div>

<style>
  [data-tauri-drag-region] {
    -webkit-app-region: drag;
    app-region: drag;
  }

  button,
  label,
  a {
    -webkit-app-region: no-drag;
    app-region: no-drag;
  }
</style>
