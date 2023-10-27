<template>
  <transition name="fade-up-in" appear>
    <div
      v-if="shown && (!isIOS && !isInStandaloneMode)"
      class="pwa-prompt"
      :class="[{ shown }]"
    >
      Add app to home screen?

      <button class="install-button" @click="installPWA">
        Install!
      </button>

      <button class="close-button" @click="dismissPrompt">
        <span aria-hidden="true">×</span>
        <!-- Accessible text, so screen readers don't just read a symbol -->
        <span class="sr">Dismiss without installing</span>
      </button>
    </div>
  </transition>
</template>


<script>
export default {
  data: () => ({
    installEvent: undefined,
    shown: false,
    isIOS: false,
    isInStandaloneMode: false,
  }),

  beforeMount() {
    this.checkIOS()
    this.checkStandaloneMode()
    window.addEventListener('beforeinstallprompt', (e) => {
      e.preventDefault()
      this.installEvent = e
      this.shown = true
    })
  },

  methods: {
    installPWA() {
      this.installEvent.prompt()
      this.installEvent.userChoice.then((choice) => {
        this.dismissPrompt() 
        if (choice.outcome === 'accepted') {
          // Do something additional if the user chose to install
        } else {
          // Do something additional if the user declined
        }
      })
    },

    dismissPrompt() {
      this.shown = false
    },

    checkIOS() {
      const userAgent = window.navigator.userAgent.toLowerCase();
      this.isIOS = /iphone|ipad|ipod/.test(userAgent);
    },

    checkStandaloneMode() {
      this.isInStandaloneMode = ('standalone' in window.navigator) && (window.navigator.standalone);
    },
  }
}
</script>


<style scoped lang="scss">
.pwa-prompt {
  position: fixed;
  font-size: 1.25rem;
  z-index: 20;
  line-height: 1;
  bottom: 0;
  left: 0;
  width: 100vw;
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 4rem;
  background: var(--dark);
  color: var(--background);
  transform: translateY(0);
  margin: 0;

  .install-button {
    font-size: inherit;
    margin: 0 0 0 0.5rem;
    padding: 0.25em 0.5em;
    background-color: var(--bright);
    border: 0;
    border-radius: 4px;
    line-height: 1;
    text-transform: uppercase;
    font-weight: 600;
  }

  .close-button {
    position: absolute;
    right: 0;
    top: -1.7rem;
    font-size: 2rem;
    background: black;
    border: 0;
    padding: 0 0.2rem;
    border-radius: 50%;
    height: 40px;
    line-height: 1;
  }

  // For the accessible text. Most projects have their own .sr-only class or similar in the base styles.
  .sr {
    position: absolute;
    width: 1px;
    height: 1px;
    left: -100vw;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0,0,0,0);
    border: 0;
  }
}

.fade-up-in-enter-active, .fade-up-in-leave-active {
  transition: opacity 1s cubic-bezier(0.165, 0.84, 0.44, 1), transform 1s cubic-bezier(0.165, 0.84, 0.44, 1);
  transform: translateY(0);
}

.fade-up-in-enter, .fade-up-in-leave-to {
  opacity: 0;
  transform: translateY(4rem);
}
</style>