<template>
  <div v-if="Object.keys(paraminfo).length !== 0" class="params-wrap">
    <div v-for="(item, index) in paraminfo.rule">
      <div v-for="(list, index) in item" class="flex">
        <div v-for="(listitem, index) in list" class="rule-list-item">
          {{ listitem }}
        </div>
      </div>
    </div>
    <div v-for="(info, index) in paraminfo.info" :key="index" class="flex info-list-wrap">
      <div class="info-list-tit">{{ info.key }}</div>
      <div class="value">{{ info.value }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "detailparmsinfo",
  props: {
    paraminfo: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style scoped>
.params-wrap {
  border-top: 4px solid #ececec;
  border-bottom: 4px solid #ececec;
}

.rule-list-item {
  font-size: 12px;
  width: 20%;
  border-bottom: 1px solid #ececec;
  padding: 10px 4px;
}

.info-list-wrap {
  font-size: 14px;;
  border-bottom: 1px solid #ececec;
  padding: 10px 4px;
  line-height: 20px;
}
.info-list-tit {
  width: 18%;
}
.value{
  color: var(--color-text);
}
</style>