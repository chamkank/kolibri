<template>

  <core-modal :title="$tr('deleteExam')" @cancel="close">
    <p v-html="$trHtml('areYouSure', { examTitle })"></p>
    <div class="footer">
      <icon-button :text="$tr('cancel')" @click="close"/>
      <icon-button :text="$tr('delete')" :primary="true" @click="deleteExam(examId)"/>
    </div>
  </core-modal>

</template>


<script>

  const examActions = require('../../state/actions/exam');

  module.exports = {
    $trNameSpace: 'deleteExamModal',
    $trs: {
      deleteExam: 'Delete exam',
      areYouSure: 'Are you sure you want to delete <strong>{ examTitle }</strong>? You will lose all data for this exam.',
      cancel: 'Cancel',
      delete: 'Delete',
    },
    components: {
      'core-modal': require('kolibri.coreVue.components.coreModal'),
      'icon-button': require('kolibri.coreVue.components.iconButton'),
    },
    props: {
      examId: {
        type: String,
        required: true,
      },
      examTitle: {
        type: String,
        required: true,
      },
      classId: {
        type: String,
        required: true,
      },
    },
    methods: {
      close() {
        this.displayExamModal(false);
      },
    },
    vuex: {
      actions: {
        displayExamModal: examActions.displayExamModal,
        deleteExam: examActions.deleteExam,
      },
    },
  };

</script>


<style lang="stylus" scoped>

  .footer
    text-align: center
    button
      min-width: 45%

</style>

