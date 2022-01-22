<template>
  <div id="app">
    <div class="header">Profiles List</div>
    <div class="content">
      <div class="buttons">
        <button @click="sortAsc">▲ <small><br/>By likes</small></button>
        <button @click="sortDesc">▼ <small><br/>By likes</small></button>
        <button @click="sortByNameAsc">▲ <small><br/>By name</small></button>
        <button @click="sortByNameDesc">▼ <small><br/>By name</small></button>
        <button @click="toggleProfileAdd">
          <small :class="addProfile ? 'hidden' : ''">Add Profile</small>
          <small :class="!addProfile ? 'hidden' : ''">Stored Profiles</small>
        </button>
      </div>
      <div class="add-profile" :class="!addProfile ? 'hidden' : ''">
        <p>Add new profile</p>
        <p>
          <label for="prof-name">Profile Name</label>
          <input v-model="prof.name" placeholder="Profile name" id="prof-name" />
        </p>
        <p>
          <label for="prof-name">Profile Email</label>
          <input type="email" v-model="prof.email" placeholder="Profile name" id="prof-name" />
        </p>
        <p>
          <label for="prof-description">Profile Description</label>
          <textarea v-model="prof.description" placeholder="Profile name" id="prof-description"></textarea>
        </p>
        <p>
          <button @click="addNewProfile">Add Profile</button>
        </p>
      </div>
      <div :class="addProfile ? 'hidden' : ''">
        <ProfileCard
          v-for="(profile, index) in profiles"
          :key="index"
          :profile="profile"
          class="profile"
        />
      </div>
      <div class="icons-note">
        Icons made by
        <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from
        <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a>
      </div>
    </div>
  </div>
</template>

<script>
import ProfileCard from "./components/ProfileCard";

export default {
  name: "App",

  components: {
    ProfileCard
  },

  data() {
    return {
      profiles: [
        {
          id: 1,
          name: "Wojciech",
          email: "wojciech@poz.pl",
          description: "Anaesthesiologist",
          likes: 34,
          comment: 'Hi woj'
        },
        {
          id: 2,
          name: "Maria",
          email: "maria@poz.pl",
          description: "Radiologist",
          likes: 28,
          comment: "I am Maria"
        },
        {
          id: 3,
          name: "Anna",
          email: "anna@poz.pl",
          description: "Surgeon",
          likes: 53,
          comment: "Nice to be Anna"
        }
      ],
      addProfile: false,
      prof: {
        name: '', email: '', description: ''
      }
    };
  },

  methods: {
    sortAsc() {
      this.profiles.sort(function(a, b) {
        return a.likes - b.likes;
      });
    },
    sortDesc() {
      this.profiles.sort(function(a, b) {
        return b.likes - a.likes;
      });
    },
    sortByNameAsc() {
      this.profiles.sort(function(a, b) {
        if (a.name.toLowerCase() < b.name.toLowerCase()) {
            return -1;
        }
        if (a.name.toLowerCase() > b.name.toLowerCase()) {
            return 1;
        }
        return 0;
      });
    },
    sortByNameDesc() {
      this.profiles.sort(function(a, b) {
        if (b.name.toLowerCase() < a.name.toLowerCase()) {
            return -1;
        }
        if (b.name.toLowerCase() > a.name.toLowerCase()) {
            return 1;
        }
        return 0;
      });
    },
    toggleProfileAdd() {
      this.addProfile = !this.addProfile;
    },
    addNewProfile() {
      if(!this.prof.name) {
        alert('The name field is required');
      }
      else if(!this.prof.email) {
        alert('The email field is required');
      }
      else if(!this.prof.description) {
        alert('The description field is required');
      } else {
        this.profiles.push({
          id: (this.profiles.length + 1),
          name: this.prof.name,
          email: this.prof.email,
          description: this.prof.description,
          likes: 0,
          comment: ''
        });

        this.addProfile = !this.addProfile;
      }
    }
  }
};
</script>

<style lang="css">
html, body {
  margin: 0;
}
#app {
  font-family: "Roboto", helvetica, arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  padding: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  position: relative;
  background: linear-gradient(
    135deg,
    rgba(65, 184, 131, 0.9),
    rgba(52, 73, 94, 0.9)
  );
  font-size: 1.5em;
  height: 87.3vh;
  overflow: auto;
}

.hidden {
  display: none;
}

.add-profile {
  margin-top: 1em;
}
.add-profile p {
  text-align: left;
  padding: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.add-profile p label {
  font-size: 1.2rem;
  padding: .2em 0;
}
.add-profile p input, .add-profile p textarea {
  border: thin solid #35c3c1;
  border-radius: 5px;
  font-size: 1.2rem;
}
.add-profile p:first-child {
  text-align: center;
}

button {
  display: block;
  padding: 1em;
  width: 100%;
  background-color: #41B883;
  border: 1px solid;
  color: #fff;
  cursor: pointer;
  font-size: 0.75em;
  font-weight: 600;
  text-shadow: 0 1px 0 rgba(black, 0.2);
}

.content {
  width: 100%;
  min-width: 300px;
  padding: 2em;
  /* margin-top: 30px; */
  position: relative;
  background: rgba(0, 0, 0, 0.15);
}

@media screen and (min-width: 600px) {
  .content {
    /* width: 60vw; */
    max-width: 23em;
  }
}

.content::before {
  content: "";
  position: absolute;
  top: -2px;
  left: 0;
  height: 2px;
  width: 100%;
  background: #35c3c1;
}

.buttons {
  display: flex;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.25), 0 5px 5px rgba(0, 0, 0, 0.22);
}

.profile {
  margin-top: 20px;
}

.icons-note {
  margin-top: 30px;
  font-size: 10px;
}
</style>
