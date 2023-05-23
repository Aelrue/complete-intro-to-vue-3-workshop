<!-- our JS -->
<script>
export default {

  data() {
            return {
              count: 10,
              counterTitle: "Counter Standard",
              increaseAmount: 8,
              // reactive data message. Rendered with curly brace syntax in div above
              message: "Hello it works!",

              listOfNumbers: [
                { name: 1, id: "123", list: [1, 2, 3] },
                { name: 2, id: "456", list: [1, 2, 3] },
                { name: 3, id: "789", list: [1, 2, 3] },
                { name: 4, id: "101112", list: [1, 2, 3] },
                { name: 5, id: "131416", list: [1, 2, 3] },
              ],
            };
          },
          computed: {
            displayTitle() {
              if (this.count > 20) {
                return "Counter Standard - Very Long";
              } else {
                return "Counter Standard";
              }
            },
            optimizedIncreaseAmount() {
              return this.displayTitle.length * this.increaseAmount;
            },
          },
          methods: {
            increaseCount(newAmount, event) {
              // if we did: this.increaseAmount = event.target.value, we would see the counter simply tacking on the "Increase By:" number to the end of the count as it is a string. We could use Number(this.increaseAmount = event.target.value) and it would work, but it it would be a round-about way of doing things. Instead, we can used v-model in our input
              console.log(newAmount);
              console.log(event);
              this.count += this.optimizedIncreaseAmount;
            },
          },
          // watch: {
          //   count(newValue) {
          //     if (newValue > 20) {
          //       this.counterTitle += "Very Long";
          //     }
          //   },
          //
}
</script>

<!-- our HTML -->
<template>
   <h1>{{displayTitle}}</h1>
      <p :data-increment-by="increaseAmount">{{count}}</p>
      <button v-on:click="increaseCount">Increase Count</button>
      <h1>{{increaseAmount}}</h1>
      
      <p>{{optimizedIncreaseAmount}}</p>
      <div>
        <label for="increaseAmount">Increase By:</label>
        <!-- telling Vue: on input event, run function changeIncreaseAmount -->
        <!-- we could use v-bind:value="increaseAmount"
          v-on:input="changeIncreaseAmount", but v-model configures that under the hood for us -->
        <input type="number" v-model="increaseAmount" />
      </div>
      <hr />
      <p v-if="message.length % 2 === 0">Even: {{message.toUpperCase()}}</p>
      <p v-else>Odd: {{message}}</p>
      <ul v-for="(, index) in listOfNumbers" :key=" 'item-${index}'">
        <li>
          {{item.id}}
          <ul>
            <li v-for="(, index) in item.list" :key="'number-${index}'">{{number}}</li>
          </ul>
        </li>
      </ul>
</template>

