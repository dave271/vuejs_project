<script>
import chart from "./components/chart";
import db from "./components/firebaseInit";
export default {
  name: "App",

  components: {
    chart
  },

  data() {
    return {
      users: []
    };
  },

  created() {
    db.collection("users")
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          console.log(doc.data());
          const data = {
            id: doc.id,
            name: doc.data().name,
            age: doc.data().age,
            blood_group: doc.data().blood_group
          };
          this.users.push(data);
        });
      });
  }
};
</script>

<template>
  <div class="container">
    <div class="col-md-10">
      <chart></chart>
    </div>
  </div>
</template>
