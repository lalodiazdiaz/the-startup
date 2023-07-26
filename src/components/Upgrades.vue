<template>
  <div class="upgrades">
    <div class="upgrade" v-for="(upgrade, index) in upgrades" :key="index">
      <button
        :class="`button ${upgrade.disabled ? 'disabled' : ''}`"
        @click="buyUpgrade($event, index)"
      >
        {{ upgrade.name }}
        {{ upgrade.disabled ? `(lvl: ${upgrade.unlocksAt})` : "" }}
      </button>
      <div class="details">
        <div class="cost">Cost: {{ upgrade.cost }}</div>
        <div class="quantity">Quantity: {{ upgrade.quantity }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Upgrades",
  computed: {
    upgrades() {
      return this.$store.getters.availableUpgrades;
    },
  },
  methods: {
    buyUpgrade(event, index) {
      if (event.screenX > 0) {
        this.$store.commit("buyUpgrade", {
          index,
          amount: 1,
        });
      }
    },
  },
};
</script>

<style lang="scss">
.upgrades {
  background-color: #222;
  padding: 25px;
  margin: 0px 5px;

  .upgrade {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0px -15px 15px;

    .button,
    .cost,
    .quantity {
      color: #fff;
      margin: 0 15px;
    }

    .details {
      flex: 1 1 100%;

      @media (min-width: 1020px) {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;

        .cost,
        .quantity {
          color: #fff;
          font-size: 24px;
        }
      }
    }
    .button {
      appearance: none;
      border: none;
      outline: none;
      background: none;

      display: inline-block;
      min-width: 300px;
      padding: 15px 25px;
      background-color: #28a484;

      color: #fff;
      font-size: 20px;
      font-weight: 700;
      text-align: center;
      text-transform: uppercase;

      cursor: pointer;

      &.disabled {
        color: #222;
        background-color: #ccc;
        pointer-events: none;
      }

      @media (max-width: 900px) {
        min-width: 200px;
        font-size: 15px;
      }
    }
  }
}
</style>
