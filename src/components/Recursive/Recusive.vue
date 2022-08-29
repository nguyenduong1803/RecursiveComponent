<template>
  <div class="container">
    <div class="recursive">
      <div class="wrapRecursive">
        <ListRecursive
          v-for="tree in treeArray"
          :treeItem="tree"
          :key="tree.id"
          @onAction="handleAction"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ListRecursive from "./ListRecursive.vue";

export default {
  methods: {
    handleAction(value) {
      switch (value.type) {
        case "add":
          break;
        case "delete":
          this.treeArray.forEach((item, index) => {
            if (item.id === value.id) {
              this.treeArray.splice(index, 1);
            }
          });
          break;

        default:
          break;
      }
    },
  },
  data() {
    return {
      treeArray: [
        {
          id: "1",
          departmentId: "DPM0-1",
          name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
          children: [],
          open: true,
          floor: 1,
        },
        {
          id: "2",
          departmentId: "DPM0-2",
          name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
          children: [],
          open: true,
          floor: 1,
        },
        {
          id: "3",
          departmentId: "DPM0-3",
          name: "Lorem ipsum dolor,",
          open: true,
          floor: 1,
          children: [
            {
              id: "4",
              departmentId: "DPM0-4",
              name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
              children: [],
              open: false,
              floor: 2,
            },
            {
              id: "5",
              departmentId: "DPM0-5",
              name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
              children: [
                {
                  id: "6",
                  departmentId: "DPM0-6",
                  name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
                  children: [],
                  open: false,
                  floor: 3,
                },
              ],
              open: false,
              floor: 2,
            },
            {
              id: "7",
              departmentId: "DPM0-7",
              name: "Lorem ipsum dolor,orem ipsum dolororem ipsum dolor",
              children: [
                {
                  id: "8",
                  departmentId: "DPM0-8",
                  name: "Lorem ipsum dolor,",
                  children: [
                    {
                      id: "9",
                      departmentId: "DPM0-9",
                      name: "Lorem ipsum dolor,",
                      children: [],
                      open: false,
                      floor: 4,
                    },
                  ],
                  open: false,
                  floor: 3,
                },
              ],
              open: false,
              floor: 2,
            },
          ],
        },
      ],
    };
  },
  components: {
    ListRecursive,
  },
};
</script>

<style  scoped>
.container {
  width: 477px;
  margin: 0 auto;
}
.recursive {
  padding-left: 23px;
}
</style>