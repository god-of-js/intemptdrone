<template>
  <div class="home">
    <div :class="['drone', direction]" id="drone">
      <div class="rotor-shaft">
        <span></span>
      </div>
      <div class="helix-top"></div>
      <div class="helix-bot"></div>
      <div class="body-box">
        <span></span>
        <span></span>
        <span></span>
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: () => {
    return {
      direction: "",
      drone: null,
    };
  },
  mounted() {
    window.addEventListener("keydown", (e) => {
      switch (e.code) {
        case "ArrowUp":
          this.moveUp();
          break;
        case "ArrowDown":
          this.moveDown();
          break;
        case "ArrowRight":
          this.moveRight();
          break;
        case "ArrowLeft":
          this.moveLeft();
          break;

        default:
          break;
      }
    });
    this.drone = document.getElementById("drone");
  },
  methods: {
    moveUp() {
      this.direction = "up move";
    },
    moveRight() {
      this.drone.animate(
        {
          transform: ["translateX(0vmin)", "translateX(50vmin)"],
        },
        {
          duration: 1000,
          composite: "add",
        }
      );
    },
    moveLeft() {
      this.drone.animate(
        {
          transform: ["translateX(0vmin)", "translateX(-50vmin)"],
        },
        {
          duration: 1000,
          composite: "add",
        }
      );
    },
    moveDown() {
      if (this.direction !== "") {
        this.direction = "down move";
        setTimeout(() => {
          this.direction = "";
        }, 1000);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/keyframes.scss";
.home {
  display: flex;
  justify-content: center;
}
.drone {
  width: 30vmin;
  height: 30vmin;
  position: absolute;
  perspective: 100vmin;
  transform: rotateX(0deg) rotateY(-5deg);
  transform-style: preserve-3d;
  bottom: 15vmin;
  perspective-origin: top;
  perspective-origin: bottom;
}

.rotor-shaft {
  width: 1vmin;
  height: 10vmin;
  background: linear-gradient(90deg, #212121, #555);
  position: absolute;
  left: calc(50% - 0.5vmin);
  top: 4vmin;
  z-index: -1;
}

.rotor-shaft span,
.rotor-shaft span:before,
.rotor-shaft span:after {
  background: #000;
  width: 2.5vmin;
  height: 2.5vmin;
  position: absolute;
  transform: rotateX(90deg) translate3d(-0.75vmin, 0vmin, -1vmin);
  border-radius: 100%;
  transform-style: preserve-3d;
}

.rotor-shaft span:before {
  content: "";
  background: #212121;
  transform: rotateX(0deg) translate3d(0vmin, 0vmin, 0.2vmin);
}

.rotor-shaft span:after {
  content: "";
  background: #212121;
  transform: rotateX(0deg) translate3d(0vmin, 0vmin, -0.2vmin);
}

.rotor-shaft span + span {
  top: 6vmin;
}

/*** HELIXES ***/

.helix-top,
.helix-bot {
  position: absolute;
  width: 30vmin;
  height: 3vmin;
  border-radius: 100% 0;
  top: 6vmin;
  left: calc(50% - 15vmin);
  transform: rotateX(70deg) rotateZ(0deg);
  border: 1px solid #333333;
  background-color: #121212;
  background-image: linear-gradient(
      45deg,
      black 25%,
      transparent 25%,
      transparent 75%,
      black 75%,
      black
    ),
    linear-gradient(
      -45deg,
      black 25%,
      transparent 25%,
      transparent 75%,
      black 75%,
      black
    );
  background-size: 1.15vmin 1.15vmin;
}

.helix-bot {
  top: 8vmin;
  transform: rotateX(-110deg) rotateZ(-10deg);
}

.drone .helix-top {
  // transform: none;
  box-shadow: 0 0 5px 0px #000;
}

.drone.move .helix-bot {
  animation: helix-bot-spin 0.075s 0s infinite;
}
.drone.move .helix-top {
  animation: helix-top-spin 0.085s 0s infinite;
}
.drone .helix-bot {
  // transform: none;
  box-shadow: 0 0 5px 0px #000;
}
.drone.up {
  animation: takeoff 2s ease 0s 1, flight 1s ease 1s infinite alternate;
}
.drone.down {
  animation: landing 1s ease-in 0s 1;
}
.drone.right {
  animation: moveRight 1s ease-in 0s 1;
}
.drone.right.up {
  animation: takeoff 2s ease 0s 1, flight 1s ease 1s infinite alternate,
    moveRight 1s ease-in 0s 1;
}
.body-box {
  position: absolute;
  width: 6vmin;
  height: 6vmin;
  background: #efefef;
  top: 12.5vmin;
  left: calc(50% - 2.5vmin);
  transform: translate3d(-0.5vmin, 0, -3.25vmin);
  transform-style: preserve-3d;
  z-index: -2;
}

.body-box > span {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, #bcc6cc, #eee 33%, #eee 38%, #bcc6cc);
  border: 1px solid #fff;
}

.body-box span:nth-child(1) {
  transform: rotateX(90deg) translate3d(0px, 3vmin, 3vmin);
  filter: brightness(1.05);
}

.body-box span:nth-child(2) {
  transform: rotateX(0deg) translate3d(0, 0, 6vmin);
  filter: brightness(0.95);
}

.body-box span:nth-child(3) {
  transform: rotateY(-90deg) translate3d(3vmin, 0, 3vmin);
}

.body-box span:nth-child(4) {
  transform: rotateX(-90deg) translate3d(0, -3vmin, 3vmin);
  background: radial-gradient(
      circle at 40% 40%,
      #fff 0.15vmin,
      #121212,
      transparent 0.45vmin
    ),
    radial-gradient(
      circle at 60% 40%,
      #fff 0.15vmin,
      #121212,
      transparent 0.45vmin
    ),
    radial-gradient(circle at 50% 14%, #000 0.1vmin, #333, transparent 0.25vmin),
    radial-gradient(circle at 50% 30%, #000 0.05vmin, #333, transparent 0.2vmin),
    linear-gradient(45deg, #bcc6cc, #eee 33%, #eee 38%, #bcc6cc);
}

.body-box span:nth-child(5) {
  transform: rotateY(90deg) translate3d(-3vmin, 0, 3vmin);
}

.body-box span:nth-child(6) {
  transform: rotateY(0deg) translate3d(0, 0, 0);
}

.body-box span:nth-child(1):before {
  content: "";
  background: radial-gradient(#2d2d2d, transparent 50%),
    radial-gradient(transparent, transparent 3.25vmin, #212121 3.5vmin);
  width: 100%;
  height: 100%;
  position: absolute;
}

.body-box span:nth-child(1) {
  border: 0;
}
</style>
