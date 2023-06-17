<template>
  <div class="container-fluid bg-image" style="overflow: hidden;">
    <div class="row align-items-center" style="height: 100vh;">
      <div class="col-md-12 text-center">
        <div class="content">
          <h1>{{ name }}</h1>
          <div class="typing-effect">
            <span class="text">{{ typingText }}</span>
            <span class="cursor" :class="{ 'blink-animation': showCursor }"></span>
          </div>
          <div class="social-links">
            <a href="https://github.com/LESS14" title="Github" target="_blank" draggable="false"><img src="/github-mark.svg" draggable="false"></a>
            <a href="https://www.linkedin.com/in/felipe-maciel-56b594270/" title="Linkedin" target="_blank" draggable="false"><img src="/linkedin-mark.svg" draggable="false"></a>
            <a href="https://felipe.ebxdesignstudio.com/blog/" style="font-size:14px;" title="Blog Wordpress" target="_blank" draggable="false"><img src="/wordpress-mark.svg" draggable="false"></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container-fluid {
  padding: 0;
}

.bg-image {
  background: #1d1d1d;
  background-size: cover;
  background-position: center;
}

.content {
  text-align: center;
  color: white;
  position: relative;
  z-index: 1;
}

.typing-effect {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}

.text {
  font-size: 24px;
}

.cursor {
  display: inline-block;
  width: 10px;
  height: 24px;
  background-color: white;
  margin-left: 5px;
}

.blink-animation {
  animation: blink 1s infinite;
}

.social-links {
  padding: 1rem;
  user-select: none;
}

@keyframes blink {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

@keyframes erase {
  0% {
    width: 100%;
  }
  100% {
    width: 0;
  }
}
</style>

<script>
export default {
  head: {
    title: 'Felipe - Portfólio'
  },

  data() {
    return {
      name: 'Felipe',
      typingText: '',
      showCursor: true,
      typingIndex: 0,
      typingPhrases: ['Sou um programador', 'Brogrammer', 'Desenvolvedor web'],
      currentPhraseIndex: 0
    }
  },
  mounted() {
    this.startTypingEffect();
  },
  methods: {
    startTypingEffect() {
      const type = () => {
        const currentPhrase = this.typingPhrases[this.currentPhraseIndex];
        if (this.typingIndex < currentPhrase.length) {
          this.typingText += currentPhrase.charAt(this.typingIndex);
          this.typingIndex++;
          setTimeout(type, 100);
        } else {
          setTimeout(this.eraseText, 500);
        }
      };

      this.eraseText = () => {
        if (this.typingIndex > 0) {
          this.typingText = this.typingText.slice(0, -1);
          this.typingIndex--;
          setTimeout(this.eraseText, 50);
        } else {
          this.typingText = '';
          this.typingIndex = 0;
          this.currentPhraseIndex = (this.currentPhraseIndex + 1) % this.typingPhrases.length;
          setTimeout(type, 500);
        }
      };

      setInterval(() => {
        this.showCursor = !this.showCursor;
      }, 500);

      type();
    }
  }
}
</script>
