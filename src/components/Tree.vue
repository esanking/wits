<template>
  <v-container fill-height fluid>
  <v-row
    align="center"
    justify="center">
    <v-col
      cols="12"
      sm="7"
      md="5"
      >
      <v-treeview open-on-click :items="items"> </v-treeview>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
const MainGroup = {
  fields: ['GroupID', 'ProdID'],
  kind: ['String', 'String'],
  items: [
    ['GroupAA', 'Prod1'],
    ['GroupBB', 'Prod4'],
    ['GroupAA', 'Prod2'],
  ],
};
const SubGroup = {
  fields: ['GroupID', 'ParentGroupID', 'Level'],
  kind: ['String', 'String', 'Int32'],
  items: [
    ['Prod1_1', 'Prod1', 2],
    ['Prod1_2', 'Prod1', 2],
    ['Prod1_2_1', 'Prod1_2', 3],
    ['Prod2_2', 'Prod2', 2],
  ],
};

export default {
  data: () => ({
    items: [],
    open: ['public'],
  }),
  created() {
    this.Node1();
    this.Node2();
  },
  methods: {
    Node1 () {
      let parse = [];
      MainGroup.items.forEach((element, index) => {
        if (parse.includes(element[0])) {
          this.items.forEach((item) => {
            if (item.name === element[0]) {
              item.children.push({
                id: index,
                name: element[1],
                children: [],
              });
            }
          });
        } else {
          parse.push(element[0]);
          this.items.push({
            id: index,
            name: element[0],
            children: [{ id: index, name: element[1], children: [] }],
          });
        }
      });
    },
    Node2 () {
      let Node3 = [];
      SubGroup.items.forEach((element, index) => {
        if (element[2] === 2) {
          this.items.forEach((item) => {
            item.children.forEach((children) => {
              if (children.name === element[1]) {
                children.children.push({
                  id: index,
                  name: element[0],
                  children: [],
                });
              }
            });
          });
        } else if (element[2] === 3) {
          Node3.push(element)
        }
      });
      this.Node3(Node3);
    },
    Node3 (Node3) {
      Node3.forEach((element, index) => {
        this.items.forEach((item) => {
          item.children.forEach((children) => {
            children.children.forEach((children2) => {
              if (children2.name === element[1]) {
                children2.children.push({
                  id: index,
                  name: element[0],
                  children: [],
                });
              }
            });
          });
        });
      })
    }
  },
};
</script>