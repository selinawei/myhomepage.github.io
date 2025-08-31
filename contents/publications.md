<style>
.pdf-pair{display:flex;gap:1rem;flex-wrap:wrap;margin:.4rem 0 1.1rem;}
.pdf-card{border:1px solid #d9ddf8;padding:.55rem .75rem;border-radius:8px;background:#eff1fe;font-size:.75rem;text-align:center;min-width:130px;box-shadow:0 1px 2px rgba(0,0,0,.05);} 
.pdf-card:hover{background:#e6e9fb;text-decoration:none;} 
.pdf-card svg{width:26px;height:26px;fill:#3948d2;} 
.pdf-card span{display:block;margin-top:.35rem;font-weight:600;color:#3948d2;}
.pdf-single{margin:.35rem 0 1.0rem;}
/* PDF.js 预览样式 */
.pdf-preview{margin:.75rem 0 1.25rem;position:relative;padding:0.4rem;border:1px solid #cfd3ec;border-radius:8px;background:#fff;box-shadow:0 2px 4px rgba(0,0,0,.06);}
.pdf-preview.loading:before{content:'Loading PDF...';position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);font-size:.8rem;color:#666;}
.pdf-preview canvas{display:block;width:100%!important;height:auto!important;border-radius:4px;}
.pdf-actions{margin-top:.35rem;font-size:.7rem;}
.pdf-actions a{margin-right:1rem;color:#3948d2;text-decoration:none;}
.pdf-actions a:hover{text-decoration:underline;}
@media (max-width:680px){.pdf-preview{padding:0.25rem;}}
</style>

### Publications

1. **All-in-Focus Seeing Through Occlusion with Event and Frame.** *PRCV 2025.*  
   Authors: Lixuan Wei, Yiche Liu, Kejing Xia, Huijiao Wang, Lei Yu  
   <div id="pdf-prcv" class="pdf-preview loading"></div>
   <div class="pdf-actions">
     <a href="static/assets/files/PRCV.pdf" target="_blank">在新标签打开</a>
     <a href="static/assets/files/PRCV.pdf" download>下载 PDF</a>
   </div>

2. **All-in-Focus Imaging from Events with Occlusions.** *IEEE Transactions on Multimedia.* *  
   Authors: Yichen Liu*, Lixuan Wei*, Yufei Guo, Lei Yu  
   <details open>
     <summary style="cursor:pointer;font-size:.9rem;color:#3948d2;margin-top:.4rem;">展开/收起 Part 1 & Part 2 PDF 预览</summary>
     <div id="pdf-tmm1" class="pdf-preview loading"></div>
     <div class="pdf-actions" style="margin-top:-.5rem;margin-bottom:.6rem;">
       <a href="static/assets/files/TMM1.pdf" target="_blank">Part 1 新标签</a>
       <a href="static/assets/files/TMM1.pdf" download>下载 Part 1</a>
     </div>
     <div id="pdf-tmm2" class="pdf-preview loading"></div>
     <div class="pdf-actions" style="margin-top:-.5rem;">
       <a href="static/assets/files/TMM2.pdf" target="_blank">Part 2 新标签</a>
       <a href="static/assets/files/TMM2.pdf" download>下载 Part 2</a>
     </div>
   </details>

3. **A Spatio-temporal Event Transformer on Versatile Tasks for Human Behavior Analysis.** *IJCAI Workshop.* *  
   Authors: Kejing Xia*, Lixuan Wei*, Lei Yu  
   <div id="pdf-ijcai" class="pdf-preview loading"></div>
   <div class="pdf-actions">
     <a href="static/assets/files/IJCAI.pdf" target="_blank">新标签打开</a>
     <a href="static/assets/files/IJCAI.pdf" download>下载</a>
   </div>

4. **Serving Individuals with Language Impairments using Automatic Speech Recognition Models and Large Language Models: Challenges and Opportunities.** *Nature Medicine* (under review).  
   <div class="pdf-single"><em>Preprint / manuscript PDF not publicly linked yet.</em></div>

<small>* Equal contribution.</small>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
(function(){
  const worker = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  if(window['pdfjsLib']){ pdfjsLib.GlobalWorkerOptions.workerSrc = worker; }
  const tasks = [
    { url:'static/assets/files/PRCV.pdf',  el:'pdf-prcv', pages:1 },
    { url:'static/assets/files/TMM1.pdf',  el:'pdf-tmm1', pages:1 },
    { url:'static/assets/files/TMM2.pdf',  el:'pdf-tmm2', pages:1 },
    { url:'static/assets/files/IJCAI.pdf', el:'pdf-ijcai', pages:1 }
  ];
  const renderPreview = (url, mountId, pages)=>{
    const mount = document.getElementById(mountId);
    if(!mount) return;
    pdfjsLib.getDocument(url).promise.then(pdf=>{
      mount.classList.remove('loading');
      const toRender = Math.min(pages, pdf.numPages);
      for(let p=1;p<=toRender;p++){
        pdf.getPage(p).then(page=>{
          const scale = 1.1; // 调整缩放
            const viewport = page.getViewport({ scale });
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = viewport.width; canvas.height = viewport.height;
            mount.appendChild(canvas);
            page.render({ canvasContext: ctx, viewport });
            if(p === toRender){
              // 添加半透明遮罩提示查看更多
              if(pdf.numPages > toRender){
                const more = document.createElement('div');
                more.style.cssText='position:absolute;right:10px;bottom:6px;background:rgba(0,0,0,.55);color:#fff;font-size:.65rem;padding:2px 6px;border-radius:4px;';
                more.textContent = `仅显示第 1 页 / 共 ${pdf.numPages} 页`; mount.style.position='relative'; mount.appendChild(more);
              }
            }
        });
      }
    }).catch(err=>{
      mount.classList.remove('loading');
      mount.innerHTML = '<div style="font-size:.7rem;color:#c00;">PDF 预览失败: '+ (err.message||err) +'</div>';
    });
  };
  document.addEventListener('DOMContentLoaded', ()=>{
    tasks.forEach(t=>renderPreview(t.url,t.el,t.pages));
  });
})();
</script>

