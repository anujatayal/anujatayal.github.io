---
layout: page
permalink: /cv/
title: cv
nav: true
nav_order: 4
cv_pdf: resume.pdf
description: My Curriculum Vitae
---

<!-- PDF Download Button -->
<div class="text-center mb-4">
  <a href="{{ 'assets/pdf/resume.pdf' | relative_url }}" 
     target="_blank" 
     class="btn btn-primary">
    <i class="fas fa-download"></i> Download PDF
  </a>
</div>

<!-- Embedded PDF Resume -->
<div class="pdf-container" style="width: 100%; height: 800px; margin: 20px 0; border: 1px solid #ddd; border-radius: 5px;">
  <iframe src="{{ '/assets/pdf/resume.pdf' | relative_url }}" 
          width="100%" 
          height="100%" 
          style="border: none;"
          type="application/pdf">
    <p>Your browser does not support inline PDFs. 
       <a href="{{ '/assets/pdf/resume.pdf' | relative_url }}" target="_blank">View PDF in new tab</a> or 
       <a href="{{ '/assets/pdf/resume.pdf' | relative_url }}" download>download the PDF</a>.
    </p>
  </iframe>
</div>

<!-- Alternative: Object embed for better browser support -->
<noscript>
  <object data="{{ '/assets/pdf/resume.pdf' | relative_url }}" 
          type="application/pdf" 
          width="100%" 
          height="800px">
    <p>Your browser does not support PDFs. 
       <a href="{{ '/assets/pdf/resume.pdf' | relative_url }}" target="_blank">View PDF</a>.
    </p>
  </object>
</noscript>
