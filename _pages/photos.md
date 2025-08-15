---
layout: page
permalink: /photos/
title: Photos
nav: true
nav_order: 5
---

<div class="photos">
  <!-- Photo Gallery Section -->
  <div class="photo-grid">
    {% assign photo_extensions = "jpg,jpeg,png,gif,webp" | split: "," %}
    {% assign poster_photos = "" | split: "" %}
    {% assign other_photos = "" | split: "" %}
    
    {% for static_file in site.static_files %}
      {% if static_file.path contains '/assets/img/photos/' %}
        {% assign file_extension = static_file.path | split: "." | last | downcase %}
        {% if photo_extensions contains file_extension %}
          {% unless static_file.path contains 'README' %}
            {% if static_file.basename contains 'poster' %}
              {% assign poster_photos = poster_photos | push: static_file %}
            {% else %}
              {% assign other_photos = other_photos | push: static_file %}
            {% endif %}
          {% endunless %}
        {% endif %}
      {% endif %}
    {% endfor %}
    
    {% assign sorted_photos = poster_photos | concat: other_photos %}
    {% for static_file in sorted_photos %}
      <div class="photo-item">
        <img src="{{ static_file.path | relative_url }}" 
             alt="{{ static_file.basename | replace: '_', ' ' | replace: '-', ' ' | capitalize }}" 
             class="photo-img" 
             loading="lazy"
             onclick="openModal('{{ static_file.path | relative_url }}', '{{ static_file.basename | replace: '_', ' ' | replace: '-', ' ' | capitalize }}')">
      </div>
    {% endfor %}
  </div>

  <!-- If no photos are found -->
  {% assign photo_count = 0 %}
  {% for static_file in site.static_files %}
    {% if static_file.path contains '/assets/img/photos/' %}
      {% assign file_extension = static_file.path | split: "." | last | downcase %}
      {% assign photo_extensions = "jpg,jpeg,png,gif,webp" | split: "," %}
      {% if photo_extensions contains file_extension %}
        {% unless static_file.path contains 'README' %}
          {% assign photo_count = photo_count | plus: 1 %}
        {% endunless %}
      {% endif %}
    {% endif %}
  {% endfor %}

  {% if photo_count == 0 %}
  <div class="text-center mt-5">
    <div class="alert alert-info" role="alert">
      <h4 class="alert-heading">No photos yet!</h4>
      <p>Add your photos to the <code>assets/img/photos/</code> folder to display them here.</p>
      <hr>
      <p class="mb-0">Supported formats: .jpg, .jpeg, .png, .gif, .webp</p>
    </div>
  </div>
  {% endif %}
</div>

<!-- Photo Modal -->
<div class="modal fade" id="photoModal" tabindex="-1" aria-labelledby="photoModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-lg modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="photoModalLabel">Photo</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body text-center">
        <img id="modalImage" src="" alt="" class="img-fluid">
      </div>
    </div>
  </div>
</div>

<style>
.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  grid-gap: 16px;
  grid-auto-rows: 10px;
  padding: 20px 0;
}

.photo-item {
  cursor: pointer;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  background: #fff;
}

.photo-item:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.15);
}

.photo-img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
  transition: all 0.3s ease;
}

.photo-item:hover .photo-img {
  transform: scale(1.02);
}

/* Responsive breakpoints */
@media (max-width: 768px) {
  .photo-grid {
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    grid-gap: 12px;
    padding: 15px 0;
  }
}

@media (max-width: 576px) {
  .photo-grid {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-gap: 10px;
    padding: 10px 0;
  }
  
  .photo-item {
    border-radius: 8px;
  }
}

/* Dark theme support */
@media (prefers-color-scheme: dark) {
  .photo-item {
    background: #2d2d2d;
    box-shadow: 0 4px 12px rgba(255, 255, 255, 0.05);
  }
  
  .photo-item:hover {
    box-shadow: 0 12px 32px rgba(255, 255, 255, 0.1);
  }
}

/* Modal improvements */
.modal-content {
  border-radius: 12px;
  border: none;
}

.modal-body {
  padding: 0;
}

#modalImage {
  border-radius: 8px;
  max-height: 80vh;
  object-fit: contain;
}

.btn-close {
  position: absolute;
  top: 15px;
  right: 15px;
  z-index: 1050;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 50%;
  width: 32px;
  height: 32px;
}
</style>

<script>
// Initialize masonry layout after images load
document.addEventListener('DOMContentLoaded', function() {
  const grid = document.querySelector('.photo-grid');
  if (!grid) return;
  
  // Function to set up masonry layout
  function setupMasonry() {
    const items = grid.querySelectorAll('.photo-item');
    const gap = 16;
    
    items.forEach((item, index) => {
      const img = item.querySelector('.photo-img');
      if (img.complete) {
        positionItem(item, index);
      } else {
        img.addEventListener('load', () => positionItem(item, index));
      }
    });
  }
  
  function positionItem(item, index) {
    if (window.innerWidth <= 576) {
      // Simple layout for mobile
      item.style.gridRowEnd = 'auto';
      return;
    }
    
    const img = item.querySelector('.photo-img');
    const aspectRatio = img.naturalHeight / img.naturalWidth;
    const baseHeight = 200;
    const calculatedHeight = Math.round(baseHeight * aspectRatio);
    const spans = Math.ceil((calculatedHeight + 16) / 10);
    
    item.style.gridRowEnd = `span ${Math.max(spans, 15)}`;
  }
  
  // Setup masonry when page loads
  setupMasonry();
  
  // Re-setup on window resize
  let resizeTimer;
  window.addEventListener('resize', function() {
    clearTimeout(resizeTimer);
    resizeTimer = setTimeout(setupMasonry, 250);
  });
});
</script>

<script>
function openModal(imageSrc, imageAlt) {
  document.getElementById('modalImage').src = imageSrc;
  document.getElementById('modalImage').alt = imageAlt;
  document.getElementById('photoModalLabel').textContent = imageAlt;
  
  // Bootstrap 5 modal
  if (typeof bootstrap !== 'undefined') {
    const modal = new bootstrap.Modal(document.getElementById('photoModal'));
    modal.show();
  } else {
    // Fallback for Bootstrap 4 or if Bootstrap JS is not loaded
    $('#photoModal').modal('show');
  }
}
</script>
