<script setup lang="ts">
import './NotoSansCJKsc-normal'
import jsPDF from "jspdf";
import {onMounted} from "vue";

function genPdf() {
  const doc = new jsPDF();
  doc.setFontSize(40);
  doc.setFont("NotoSansCJKsc");

  // japanese
  doc.text("天気がいいから 散歩しましょう", 5, 25);
  // chinese
  doc.text("是中文呀", 5, 65);
  // korean
  doc.text("안녕하세요, 만나서 반갑습니다", 5, 105);

  //doc.output('pdfobjectnewwindow')
  return doc
}

onMounted(() => {
  const frame = document.getElementById("pdfFrame") as HTMLIFrameElement
  const pdf = genPdf()
  frame.src = pdf.output('dataurlstring')
})

function handleDownload() {
  const pdf = genPdf()
  pdf.save("cjk.pdf")
}
</script>

<template>
  <div>
    <button style="display: block;" @click="handleDownload">Download</button>
    <iframe id="pdfFrame" style="width: 600px;height: 800px;margin-top: 8px"/>
  </div>
</template>
