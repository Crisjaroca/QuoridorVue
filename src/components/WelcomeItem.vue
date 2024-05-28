<template>
  <div class="welcome-item">
    <i class="welcome-item__icon">
      <slot name="icon"></slot>
    </i>
    <div class="welcome-item__details">
      <h3 class="welcome-item__heading">
        <slot name="heading"></slot>
      </h3>
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.welcome-item {
  margin-top: 2rem;
  display: flex;
  position: relative;
}

.welcome-item__details {
  flex: 1;
  margin-left: 1rem;
}

.welcome-item__icon {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;
  color: var(--color-text);
}

.welcome-item__heading {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

@media (min-width: 1024px) {
  .welcome-item {
    margin-top: 0;
    padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
  }

  .welcome-item__icon {
    top: calc(50% - 25px);
    left: -26px;
    position: absolute;
    border: 1px solid var(--color-border);
    background: var(--color-background);
    border-radius: 8px;
    width: 50px;
    height: 50px;
  }

  .welcome-item:before {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    bottom: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .welcome-item:after {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    top: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .welcome-item:first-of-type:before {
    display: none;
  }

  .welcome-item:last-of-type:after {
    display: none;
  }
}
</style>
