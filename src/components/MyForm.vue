<template>
  <div>
    <form>
      <div v-for="(field, id) in myData?.fields" :key="id">
        <label :for="field?.name">{{ field?.name }}</label>
        <component :is="field?.component" />
        <div>
          <label v-for="option in field?.options" :key="option.value">
            <input type="radio" v-model="$attrs.value" :name="field?.name" />
            {{ option.label }}
          </label>
        </div>
        <button>shubham</button>
      </div>
    </form>
  </div>
</template>

<script>
import yaml from "js-yaml";
export default {
  name: "MyComponent",
  data() {
    return {
      myData: null,
    };
  },
  async mounted() {
    const response = await fetch("/assets/data.yaml");
    const text = await response.text();
    const data = yaml.load(text); //converts YAML synta to json form (load)
    this.myData = data;
  },
};
</script>
