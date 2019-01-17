<template>
  <v-card flat color="transparent">
    <v-subheader>Min and max range slider</v-subheader>

    <v-card-text>
      <v-layout row>
          <v-range-slider
            v-model="test"
            :max=10
            :min=0
            :step="1"
          ></v-range-slider>
      </v-layout>

      <v-layout row v-for="(range, i) in rangeValues" :key="i">
        <v-flex shrink style="width: 60px">
          <v-text-field
            v-model="range[0]"
            class="mt-0"
            hide-details
            single-line
            type="number"
          ></v-text-field>
        </v-flex>

        <v-flex class="px-3">
          <v-range-slider
            v-model="rangeValues[i]"
            :max="max"
            :min="min"
            :step="1"
            ticks
            tick-size="4"
            thumb-label
            @input="inputRange(i)"
          ></v-range-slider>
        </v-flex>

        <v-flex shrink style="width: 60px">
          <v-text-field
            v-model="range[1]"
            class="mt-0"
            hide-details
            single-line
            type="number"
          ></v-text-field>
        </v-flex>
      </v-layout>

      <v-layout row>
        <v-btn fab dark small color="gray" @click="deleteRange">
          <v-icon dark>remove</v-icon>
        </v-btn>
        <v-btn fab dark small color="primary" @click="addRange">
          <v-icon dark>add</v-icon>
        </v-btn>
      </v-layout>
    </v-card-text>
  </v-card>
</template>

<script>
  export default {
    data: () => ({
      min: 1,
      max: 10,
      test: [0, 1],
      rangeValues: [[1, 3], [3, 4], [4, 10]]
    }),
    methods: {
      inputRange(i) {
        if(this.rangeValues){
          this.$set(this.rangeValues[0], 0, this.min);
          this.$set(this.rangeValues[this.rangeValues.length - 1], 1, this.max);
          if(i > 0){
            this.$set(this.rangeValues[i-1], 1, this.rangeValues[i][0]);
          }
          if(i < this.rangeValues.length - 1){
            this.$set(this.rangeValues[i+1], 0, this.rangeValues[i][1]);
          }
        }
      },
      addRange() {
        this.rangeValues.push([this.rangeValues[this.rangeValues.length-1][1], this.max]);
      },
      deleteRange() {
        if(this.rangeValues.length > 1){
          this.rangeValues.pop();
        }
      },
      // validateRules(i) {
        // return [
        //   v => (v[0] == this.min || i > 0) || 'min value',
        //   v => (v[0] == this.rangeValues[i-1][1] || i == 0) || `ranges have a space`,
        //   v => (v[1] == this.max || i < this.rangeValues.length - 1) || 'max value',
        // ];
      // }
    }
  }
</script>

<style>
</style>
