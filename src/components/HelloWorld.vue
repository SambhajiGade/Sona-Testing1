<template>
  <!-- <v-container> -->

  <v-app>
    <v-card color="#90CAF9" width="400">
      <v-card-title> Welcome to Sona Testing </v-card-title>

      <v-card-text class="pb-2">
        <v-text-field label="Email" solo></v-text-field>

        <v-text-field
          :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]"
          :type="show3 ? 'text' : 'password'"
          name="input-10-2"
          label="Password"
          hint="At least 8 characters"
          solo
          class="input-group--focused"
          @click:append="show3 = !show3"
        ></v-text-field>
      </v-card-text>

      <v-divider class="mx-4"></v-divider>

      <v-card-text class="text-center text-h6">
        <b>OR</b>
      </v-card-text>

      <v-card-text class="text-center">
        <img src="../assets/google.png" alt="" width="60" height="50" />
        <img src="../assets/link.png" alt="" width="60" height="50" />
      </v-card-text>

      <v-card-actions class="justify-center">
        <v-btn
          flat
          dark
          color="blue darken-1 text-white px-10 mb-5"
          to="/Home/"
        >
          Sign In
        </v-btn>
      </v-card-actions>
    </v-card>

    <!-- <v-form>

      <input type="file" @change="filechange" />
    </v-form>

    <v-btn max-width="5%" @click="uploadfile()">upload</v-btn>

    <v-img src="https://firebasestorage.googleapis.com/v0/b/project-360e7.appspot.com/o/data%2FScreenshot%202023-01-12%20202751.png?alt=media&token=a1830980-693b-4e8e-9958-5d9063952108"></v-img> -->
  </v-app>
  <!-- </v-container> -->
</template>

<style>
html {
  overflow-y: auto;
}
</style>

<!-- REQUIRED SCRIPTS  -->


<!-- <script src="https://www.gstatisejs/c.com/firebasejs/9.15.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/fireba9.15.0/firebase-storage.js"></script> -->

<!-- <script src="firebase/app"></script>
<script src="firebase/storage"></script> -->

<script>
// import axios from "axios";
// import firebase from 'firebase'

// import {storage} from "firebase";
// import {ref , uploadBytes} from "firebase/storage";

// import {firestore as db}  from './firebase-config' 
// import firebase from 'firebase';

// import {db} from './firebase'



// import { initializeApp } from "firebase/app";
// import { getFirestore } from 'firebase/firestore/';
// import { getAnalytics } from "firebase/analytics";



// import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
//   import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-analytics.js";
  // import firebase from 'firebase'

// const firebaseConfig = {
//   apiKey: "AIzaSyB4_XcLML_dAD1HenoVnxFaMYmBQU7G-_k",
//   authDomain: "projectmain-2ee04.firebaseapp.com",
//   projectId: "projectmain-2ee04",
//   storageBucket: "projectmain-2ee04.appspot.com",
//   messagingSenderId: "620079050243",
//   appId: "1:620079050243:web:6ac9b0f5ae23514ef3e836",
//   measurementId: "G-KCJWK56R69"
// };

// // Initialize Firebase
// const app = initializeApp(firebaseConfig);
// const db = getFirestore(app);

// const analytics = getAnalytics(app);




// import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
//   import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-analytics.js";
 
//   const firebaseConfig = {
//     apiKey: "AIzaSyB4_XcLML_dAD1HenoVnxFaMYmBQU7G-_k",
//     authDomain: "projectmain-2ee04.firebaseapp.com",
//     projectId: "projectmain-2ee04",
//     storageBucket: "projectmain-2ee04.appspot.com",
//     messagingSenderId: "620079050243",
//     appId: "1:620079050243:web:6ac9b0f5ae23514ef3e836",
//     measurementId: "G-KCJWK56R69"
//   };

//   // Initialize Firebase
//   const app = initializeApp(firebaseConfig);
//   const analytics = getAnalytics(app);


// import { initializeApp } from "firebase/app";

import * as firebase from 'firebase/app'

// import * as store from 'firebase/storage'

// import {getStorage , ref as sref , uploadBytesResumable,getDownloadURL} from 'firebase/storage'

import { getStorage, ref, uploadBytesResumable ,getDownloadURL} from "firebase/storage";
 

const firebaseConfig = {
  apiKey: "AIzaSyBsAdm3QQTHlmwMihKSaXcEjcx-cwOeX8c",
  authDomain: "project-360e7.firebaseapp.com",
  projectId: "project-360e7",
  storageBucket: "project-360e7.appspot.com",
  messagingSenderId: "921356772970",
  appId: "1:921356772970:web:362f876a5d94e3ae280c13"
};

// Initialize Firebase
 firebase.initializeApp(firebaseConfig);


export default {
  data() {
    return {
      dialog: true,
      items: [
        { title: "Institute" },
        { title: "Employer" },
        { title: "Student" },
      ],
samurl:'',
      selectedfile: null,
      show3: false,
      uploadValue:0,
      img1:null,
      password: "Password",
      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
      },
    };

    
  },

  // firestore(){
  //     return{
  //       folder:db.collection('folder'),
  //     }
  //   },

  methods: {
    filechange(event) {
      this.selectedfile = event.target.files[0];
      console.log("Selected file : ", this.selectedfile);
      console.log("Event : ",event);
    },

     uploadfile() {




      const storage = getStorage();

      const metadata ={
  contentType : 'image/jpeg'
}

// Create a reference to 'mountains.jpg'
const mountainsRef = ref(storage, 'data/' + this.selectedfile.name);

const Task = uploadBytesResumable(mountainsRef, this.selectedfile,metadata);



Task.on('state_changed',
  (snapshot) => {
    // Get task progress, including the number of bytes uploaded and the total number of bytes to be uploaded
    const progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
    console.log('Upload is ' + progress + '% done');
    switch (snapshot.state) {
      case 'paused':
        console.log('Upload is paused');
        break;
      case 'running':
        console.log('Upload is running');
        break;
    }
  }, 
  (error) => {
    // A full list of error codes is available at
    // https://firebase.google.com/docs/storage/web/handle-errors
    switch (error.code) {
      case 'storage/unauthorized':
        // User doesn't have permission to access the object
        break;
      case 'storage/canceled':
        // User canceled the upload
        break;

      // ...

      case 'storage/unknown':
        // Unknown error occurred, inspect error.serverResponse
        break;
    }
  }, 
  () => {
    // Upload completed successfully, now we can get the download URL
    getDownloadURL(Task.snapshot.ref).then((downloadURL) => {
      this.samurl=downloadURL;
      console.log('File available at', downloadURL);
    });
  }
);




// Task.then((snapshot) => {
//   console.log('Uploaded!');

//   console.log("snapshot : ",snapshot)
//   // getDownloadURL(Task.snapshot.ref).then((durl)=>{
//   //   console.log("url : ",durl)
//   // })

// // snapshot.ref.getDownloadURL().then(url=>{
// //   console.log("url is : ",url)
// // })

// });

console.log("mountainsRef : ",mountainsRef)

// console.log("app : ",app)
console.log("firebase : ",firebase)
// console.log("storage : ",store.ref(this.selectedfile.name))
// const ref = firebase.storage().ref();
// console.log("ref : ",ref)

// const metadata ={
//   contentType : this.selectedfile.type
// }


// const task = ref.child(this.selectedfile.name).put(this.selectedfile,metadata);

// task.then(snapshot=>snapshot.ref.getDownloadURL())
// .then(url=>{
//   console.log("url : ",url)
// })



    //  let storageRef = firebase.storage().ref()
    //  storageRef.put(this.selectedfile)







// const storageRef = ref(storage,'folder/'+this.selectedfile.name);
// uploadBytes(storageRef,this.selectedfile).then((snapshot)=>{
//   console.log("sn : ",snapshot)
// })


  //     this.img1=null;
  // const storageRef=firebase.storage().ref(`${this.selectedfile.name}`).put(this.selectedfile);
  // storageRef.on(`state_changed`,snapshot=>{
  // this.uploadValue = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
  //   }, error=>{console.log(error.message)},
  // ()=>{this.uploadValue=100;
  //     storageRef.snapshot.ref.getDownloadURL().then((url)=>{
  //         this.img1 =url;
  //         console.log(this.img1)
  //       });
  //     }      
  //   );
















      // const fd = new FormData();

//      let file1 = {
//           'lastMod'    : this.selectedfile.lastModified,
//           'lastModDate': this.selectedfile.lastModifiedDate,
//           'name'       : this.selectedfile.name,
//           'size'       : this.selectedfile.size,
//           'type'       : this.selectedfile.type,
//       }

//       console.log("file1 : ",this.selectedfile,this.selectedfile.name)

//       // fd.append('file', this.selectedfile,this.selectedfile.name);
//       fd.append('file', file1,file1.name);
//       // fd.append('image',this.selectedfile)

// console.log("fd : ",fd)

// // const s = JSON.toString(fd)

// try{
//   await axios
//         .post("http://localhost:3000/D", fd)
//         .then((result) => {
//           console.log("Result : ", result);
//           console.log("fd : ", fd);
//         })
//         .catch((err) => {
//           console.log("Error : ", err);
//         });
// }
// catch(error){
//   console.log("error : ",error)
// }


// let URL="http://localhost:3000/D";

// fd.append('name', 'my-picture');
//     fd.append('file', this.selectedfile); 

//     let config = {
//       header : {
//         'Content-Type' : 'image/png'
//       }
//     }

//     let conf = JSON.stringify(config);
//     let fd1 = JSON.stringify(fd)
//     axios.post(
//       URL, 
//       fd1,
//       conf
//     ).then(
//       response => {
//         console.log('image upload response > ', response)
//       }
//     )



// const responseData = await axios.postFormDataAsJson({ "http://localhost:3000/D", fd});
//         console.log({ responseData });
//     } catch (error) {
// //also console.log(fileInput.files[0]); logs an image object
//         console.error(error);
//     }


      // axios.request(
      //           method: 'POST',
      //           url: "http://localhost:3000/D",
      //           headers: { 'Content-Type': undefined },
      //           transformRequest: function (data) {
      //               let formData = new FormData();
      //               //need to convert our json object to a string version of json otherwise
      //               // the browser will do a 'toString()' on the object which will result
      //               // in the value '[Object object]' on the server.
      //               formData.append("myJsoNData", JSON.stringify(data.myExtraData));
      //               formData.append("thumbnail", data.thumbnail)
      //               return formData;
      //           },
      //             data: {myExtraData: 'someValue', thumbnail: this.selectedfile}
      //     )
      //         }
    },
    
  },
  
  
};

</script>

