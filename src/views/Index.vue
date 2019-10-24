<template>
  <div>
    <p style="text-align: center; margin: 50px 0 20px">使用 scoped-slot 自定义数据项</p>
    <div style="text-align: center">
      <start
        style="text-align: left; display: inline-block"
        v-model="value"
        :middle-value="middleValue"
        filterable
        :left-default-checked="leftDefaultChecked"
        :middle-default-checked="middleDefaultChecked"
        :right-default-checked="rightDefaultChecked"
        :titles="titles"
        :button-texts="buttonTexts"
        :format="{
        noChecked: '${total}',
        hasChecked: '${checked}/${total}'
      }"
        @middleValueChange="middleValueChange"
        @change="handleChange"
        :data="data">
        <span slot-scope="{ option }">{{ option.key }} - {{ option.label }}</span>
        <el-button class="transfer-footer" slot="left-footer" size="small">操作</el-button>
        <el-button class="transfer-footer" slot="right-footer" size="small">操作</el-button>
      </start>
    </div>
  </div>
</template>

<style>
  .transfer-footer {
    margin-left: 20px;
    padding: 6px 5px;
  }
</style>

<script>
  import Start from "@/components/test";
  export default {
    components: {
      "start": Start
    },
    data() {
      const generateData = _ => {
        const data = [];
        for (let i = 1; i <= 15; i++) {
          data.push({
            key: i,
            label: `备选项 ${ i }`,
            children: [{
              key: '2'+i,
              label: '二级 ' + i + '-' + i,
            }]
          });
        }
        return data;
      };
      return {
        data: generateData(),
        value: [1],
        middleValue: [5, 6, 7],
        leftDefaultChecked:[2, 3],
        middleDefaultChecked:[5, 6],
        rightDefaultChecked:[1],
        titles:['Source', 'Middle', 'Target'],
        buttonTexts:['到左边', '到右边', '到上面', '到下面'],
        // value4: [1],
        renderFunc(h, option) {
          return <span>{ option.key } - { option.label }</span>;
        }
      };
    },

    methods: {
      handleChange(value, direction, movedKeys) {
        console.log(value, direction, movedKeys);
      },
      middleValueChange(value) {
        this.middleValue = value;
      }
    },
    mounted() {
      console.log(this.data)
    }
  };
</script>
