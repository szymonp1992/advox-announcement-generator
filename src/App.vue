<template>
  <div class="container mt-3">
    <h2 class="mb-3">Advox Announcement Generator</h2>
    <form>
      <div class="mb-3">
        <label for="firstUrl" class="form-label">First URL</label>
        <input
          type="text"
          class="form-control"
          id="firstUrl"
          v-model="firstUrl"
        />
      </div>
      <div class="mb-3">
        <label for="firstAnnouncement" class="form-label"
          >First announcement text</label
        >
        <input
          type="text"
          class="form-control"
          id="firstAnnouncement"
          v-model="firstAnnouncement"
        />
      </div>
      <div class="mb-3">
        <label for="secondUrl" class="form-label">Second URL - optional</label>
        <input
          type="text"
          class="form-control"
          id="secondUrl"
          v-model="secondUrl"
        />
      </div>
      <div class="mb-3">
        <label for="secondAnnouncement" class="form-label"
          >Second announcement text</label
        >
        <input
          type="text"
          class="form-control"
          id="secondAnnouncement"
          v-model="secondAnnouncement"
        />
      </div>
      <div class="mb-3">
        <label for="thirdUrl" class="form-label">Third URL - optional</label>
        <input
          type="text"
          class="form-control"
          id="thirdUrl"
          v-model="thirdUrl"
        />
      </div>
      <div class="mb-3">
        <label for="thirdAnnouncement" class="form-label"
          >Third announcement text</label
        >
        <input
          type="text"
          class="form-control"
          id="thirdAnnouncement"
          v-model="thirdAnnouncement"
        />
      </div>
      <div class="mb-3">
        <label for="color" class="form-label"
          >Announcement background color -
          <a href="https://htmlcolorcodes.com/" target="_blank"
            >HEX format required</a
          >
          - example: #5F3E37</label
        >
        <input type="text" class="form-control" id="color" v-model="color" />
      </div>
      <button
        type="submit"
        class="btn btn-primary"
        @click="generateAnnouncement"
      >
        Generate
      </button>
    </form>
    <div class="announcement-code card mt-3 mb-3">
      <div class="card-header h3">Announcement code:</div>
      <div class="card-body">
        <div class="card-text">{{ announcementCode }}</div>
      </div>
    </div>
    <div class="announcement-preview card p-2 pb-0 mb-5"></div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const firstUrl = ref("");
    const firstAnnouncement = ref("");
    const secondUrl = ref("");
    const secondAnnouncement = ref("");
    const thirdUrl = ref("");
    const thirdAnnouncement = ref("");
    const color = ref("");

    const announcementCode = ref(
      "This is the field where generated code will appear"
    );

    let announcementPreview;
    onMounted(() => {
      announcementPreview = document.querySelector(".announcement-preview");
    });

    function generateAnnouncement(event) {
      event.preventDefault();
      if (!firstUrl.value && !secondUrl.value && !thirdUrl.value) {
        announcementCode.value =
          "Nothing to display. Please insert at least first URL and first announcement text";
      } else if (!secondUrl.value && !thirdUrl.value) {
        announcementCode.value = `<p class="js-promo-box_paragraph"><a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href = "${firstUrl.value}">${firstAnnouncement.value}</a></p><style>#js-promo-box {background-color: ${color.value} !important;z-index: 100;position: fixed;width: 100%;top: 0;left: 0;}p.js-promo-box_paragraph {font-size: 1.15 rem;color: #FFFFFF;}</style>`;
      } else if (!thirdUrl.value) {
        announcementCode.value = `<p class="js-promo-box_paragraph"><a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href = "${firstUrl.value}">${firstAnnouncement.value}</a> | <a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href="${secondUrl.value}">${secondAnnouncement.value}</a></p><style>#js-promo-box {background-color: ${color.value} !important;z-index: 100;position: fixed;width: 100%;top: 0;left: 0;}p.js-promo-box_paragraph {font-size: 1.15 rem;color: #FFFFFF;}</style>`;
      } else if (firstUrl.value && secondUrl.value && thirdUrl.value) {
        announcementCode.value = `<p class="js-promo-box_paragraph"><a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href = "${firstUrl.value}">${firstAnnouncement.value}</a> | <a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href="${secondUrl.value}">${secondAnnouncement.value}</a> | <a class="announcement-anchor" style="font-weight: 400;color: #FFFFFF" href = "${thirdUrl.value}">${thirdAnnouncement.value}</a></p><style>#js-promo-box {background-color: ${color.value} !important;z-index: 100;position: fixed;width: 100%;top: 0;left: 0;}p.js-promo-box_paragraph {font-size: 1.15 rem;color: #FFFFFF;}</style>`;
      }
      announcementPreview.innerHTML = announcementCode.value;
      announcementPreview.style.textAlign = "center";
      if (!color.value) {
        announcementPreview.style.backgroundColor = "#000000";
      } else {
        announcementPreview.style.backgroundColor = color.value;
      }
    }

    return {
      firstUrl,
      firstAnnouncement,
      secondUrl,
      secondAnnouncement,
      thirdUrl,
      thirdAnnouncement,
      color,
      announcementCode,
      announcementPreview,
      generateAnnouncement,
    };
  },
};
</script>

<style>
.announcement-anchor {
  text-decoration: none;
}
.announcement-anchor:hover {
  text-decoration: underline;
}
</style>