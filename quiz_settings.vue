<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input v-model="formData.name" type="text" id="name" name="name" required />
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <textarea v-model="formData.description" id="description" name="description"></textarea>
      </div>
      <div class="form-group">
        <label for="class">Class</label>
        <select v-model="formData.class_id" id="class" name="class_id">
          <option value="">Select Class (Optional)</option>
          <option v-for="classe in classes" :key="classe.id" :value="classe.id">{{ classe.name }}</option>
        </select>
      </div>
      <div class="form-group">
        <label for="studentSelection">Student Selection</label>
        <div>
          <input type="radio" id="allStudents" v-model="studentSelection" value="all" />
          <label for="allStudents">All Students</label>
        </div>
        <div>
          <input type="radio" id="selectedStudents" v-model="studentSelection" value="selected" />
          <label for="selectedStudents">Selected Students</label>
          <select v-if="studentSelection === 'selected'" v-model="formData.student_ids" multiple id="selectedStudentsList" name="student_ids[]">
            <option v-for="student in students" :key="student.id" :value="student.id">{{ student.name }}</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label for="tries">Number of Attempts</label>
        <input v-model.number="formData.tries" type="number" id="tries" name="tries" min="1" required />
      </div>
      <div class="form-group">
        <label for="startTime">Start Time</label>
        <input v-model="formData.start_time" type="datetime-local" id="startTime" name="start_time" />
      </div>
      <div class="form-group">
        <label for="endTime">End Time</label>
        <input v-model="formData.end_time" type="datetime-local" id="endTime" name="end_time" />
      </div>
      <div class="form-group">
        <label for="quizDuration">Quiz Duration (minutes)</label>
        <input v-model.number="formData.quiz_duration" type="number" id="quizDuration" name="quiz_duration" min="1" />
      </div>
      <div class="form-group">
        <label for="questionTimeLimit">Question Time Limit (seconds)</label>
        <input v-model.number="formData.question_time_limit" type="number" id="questionTimeLimit" name="question_time_limit" min="1" />
      </div>
      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    // Pass initial data for editing or set to empty object for creating new
    formData: Object,
    // Provide options for class and student selection (replace with your data fetching logic)
    classes: Array,
    students: Array,
  },
  data() {
    return {
      studentSelection: "all", // Default selection for students
    };
  },
  methods: {
    handleSubmit() {
      // Emit an event with the form data to the parent component for submission
      this.$emit('submit-form', this.formData);
    },
  },
};
</script>

<style scoped>
/* Add basic styling for the form */
</style>
