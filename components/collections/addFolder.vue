<template>
  <modal v-if="show" @close="show = false">
    <div slot="header">
      <ul>
        <li>
          <div class="flex-wrap">
            <h3 class="title">新的目录</h3>
            <div>
              <button class="icon" @click="hideModal">
                <i class="material-icons">close</i>
              </button>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <div slot="body">
      <ul>
        <li>
          <input type="text" v-model="name" placeholder="我的新目录" />
        </li>
      </ul>
    </div>
    <div slot="footer">
      <ul>
        <li>
          <button class="icon" @click="addNewFolder">
            <i class="material-icons">add</i>
            <span>创建</span>
          </button>
        </li>
      </ul>
    </div>
  </modal>
</template>

<script>
export default {
  props: {
    show: Boolean,
    collection: Object,
    collectionIndex: Number
  },
  components: {
    modal: () => import("../../components/modal")
  },
  data() {
    return {
      name: undefined
    };
  },
  methods: {
    addNewFolder() {
      this.$store.commit("postwoman/addNewFolder", {
        folder: { name: this.$data.name },
        collectionIndex: this.$props.collectionIndex
      });
      this.hideModal();
    },
    hideModal() {
      this.$emit("hide-modal");
    }
  }
};
</script>
