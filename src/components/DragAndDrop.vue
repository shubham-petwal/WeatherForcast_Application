<template>
  <div class="bg-red-700">
    <div class="flex justify-between">
        <div @dragover.prevent class="w-60 h-52 border-4" @drop="drop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4" @drop="drop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4" @drop="drop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4" @drop="drop"></div>
    </div>
    <div class="flex justify-center p-5">
      <img
        id="logo1"
        src="https://media.licdn.com/dms/image/C560BAQHwbRGwTnVinQ/company-logo_200_200/0/1668219982472?e=1686787200&v=beta&t=qToodqrSoI1AGp4ZmJzKQjDluUnzySXYCpNmSgY-cIs"
        @dragstart="drag"
        draggable="true"
      />
      <img src="https://lh6.googleusercontent.com/-mrrgh5tN-V0/AAAAAAAAAAI/AAAAAAAAAAA/tkSB4AK-8ig/s88-p-k-no-ns-nd/photo.jpg" @dragstart="copyDrag" width="200"/>
    </div>
    <div class="flex justify-between">
        <div @dragover.prevent class="w-60 h-52 border-4 flex justify-center" @drop="copydrop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4 flex justify-center" @drop="copydrop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4 flex justify-center" @drop="copydrop"></div>
        <div @dragover.prevent class="w-60 h-52 border-4 flex justify-center" @drop="copydrop"></div>
    </div>
  </div>
  <div class=" h-screen">
    <h1>shubhaqm</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    drag(e) {
      e.dataTransfer.setData("addKisai", e.target.id);
      e.dataTransfer.setData("duplicateKisai", "https://media.licdn.com/dms/image/C560BAQHwbRGwTnVinQ/company-logo_200_200/0/1668219982472?e=1686787200&v=beta&t=qToodqrSoI1AGp4ZmJzKQjDluUnzySXYCpNmSgY-cIs");
    },
    drop(e) {
      const id = e.dataTransfer.getData("addKisai");
      e.target.appendChild(document.getElementById(id));
    },
    copyDrag(e){
        e.dataTransfer.setData("copyKisai", "https://lh6.googleusercontent.com/-mrrgh5tN-V0/AAAAAAAAAAI/AAAAAAAAAAA/tkSB4AK-8ig/s88-p-k-no-ns-nd/photo.jpg");
    },
    copydrop(e){
        const data = e.dataTransfer.getData("copyKisai")
        const image = new Image();
        image.src = data
        e.target.appendChild(image)
    }
  },
};
</script>




