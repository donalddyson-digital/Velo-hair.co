/* =====================================================
VELO HAIR CO. — Global JS
===================================================== */
(function(){
‘use strict’;

/* ––––– DEMO MODAL INTERCEPTOR ––––– */
const modal = document.getElementById(‘demoModal’);
const openModal = () => { if(modal){ modal.classList.add(‘open’); document.body.style.overflow=‘hidden’; } };
const closeModal = () => { if(modal){ modal.classList.remove(‘open’); document.body.style.overflow=’’; } };

// Intercept every booking/contact action
document.addEventListener(‘click’, (e) => {
const t = e.target.closest(’[data-demo], .js-book, .js-contact, a[href^=“tel:”], a[href^=“mailto:”]’);
if(!t) return;
// allow explicit bypass (like footer credit link)
if(t.hasAttribute(‘data-allow’)) return;
e.preventDefault();
openModal();
});

// Intercept form submissions
document.querySelectorAll(‘form[data-demo-form]’).forEach(f => {
f.addEventListener(‘submit’, (e) => { e.preventDefault(); openModal(); });
});

// Modal close
if(modal){
modal.addEventListener(‘click’, (e) => { if(e.target === modal || e.target.closest(’.modal-close’)) closeModal(); });
document.addEventListener(‘keydown’, (e) => { if(e.key === ‘Escape’) { closeModal(); closeLightbox(); } });
}

/* ––––– NAV: scroll state + mobile toggle ––––– */
const nav = document.querySelector(’.nav’);
const onScroll = () => {
if(!nav) return;
if(window.scrollY > 30) nav.classList.add(‘scrolled’);
else nav.classList.remove(‘scrolled’);
};
window.addEventListener(‘scroll’, onScroll, {passive:true});
onScroll();

const toggle = document.querySelector(’.nav-toggle’);
const navLinks = document.querySelector(’.nav-links’);
if(toggle && navLinks){
toggle.addEventListener(‘click’, () => {
toggle.classList.toggle(‘open’);
navLinks.classList.toggle(‘open’);
});
navLinks.querySelectorAll(‘a’).forEach(a => a.addEventListener(‘click’, () => {
toggle.classList.remove(‘open’); navLinks.classList.remove(‘open’);
}));
}

/* ––––– SCROLL REVEAL ––––– */
const reveals = document.querySelectorAll(’.reveal’);
if(‘IntersectionObserver’ in window){
const io = new IntersectionObserver((entries) => {
entries.forEach(e => {
if(e.isIntersecting){
e.target.classList.add(‘in’);
io.unobserve(e.target);
}
});
}, { threshold: 0.12, rootMargin: ‘0px 0px -60px 0px’ });
reveals.forEach(r => io.observe(r));
} else {
reveals.forEach(r => r.classList.add(‘in’));
}

/* ––––– HERO LOAD ANIMATION ––––– */
const hero = document.querySelector(’.hero’);
if(hero) requestAnimationFrame(() => hero.classList.add(‘loaded’));

/* ––––– GALLERY FILTER ––––– */
const filterBtns = document.querySelectorAll(’.filter-btn’);
const masonryItems = document.querySelectorAll(’.masonry-item’);
filterBtns.forEach(btn => {
btn.addEventListener(‘click’, () => {
const cat = btn.dataset.filter;
filterBtns.forEach(b => b.classList.remove(‘active’));
btn.classList.add(‘active’);
masonryItems.forEach(item => {
const match = cat === ‘all’ || item.dataset.cat === cat;
item.classList.toggle(‘hidden’, !match);
});
});
});

/* ––––– LIGHTBOX ––––– */
const lb = document.getElementById(‘lightbox’);
const lbImg = lb ? lb.querySelector(‘img’) : null;
let lbItems = [];
let lbIndex = 0;

const openLightbox = (index) => {
lbItems = Array.from(document.querySelectorAll(’.masonry-item:not(.hidden) img’));
if(!lbItems.length || !lb) return;
lbIndex = index;
lbImg.src = lbItems[lbIndex].src;
lbImg.alt = lbItems[lbIndex].alt;
lb.classList.add(‘open’);
document.body.style.overflow=‘hidden’;
};
const closeLightbox = () => { if(lb){ lb.classList.remove(‘open’); document.body.style.overflow=’’; } };
const lbStep = (dir) => {
if(!lbItems.length) return;
lbIndex = (lbIndex + dir + lbItems.length) % lbItems.length;
lbImg.src = lbItems[lbIndex].src;
lbImg.alt = lbItems[lbIndex].alt;
};

document.querySelectorAll(’.masonry-item’).forEach((item, i) => {
item.addEventListener(‘click’, () => openLightbox(
Array.from(document.querySelectorAll(’.masonry-item:not(.hidden)’)).indexOf(item)
));
});

if(lb){
lb.querySelector(’.lightbox-close’).addEventListener(‘click’, closeLightbox);
lb.querySelector(’.lightbox-prev’).addEventListener(‘click’, (e) => { e.stopPropagation(); lbStep(-1); });
lb.querySelector(’.lightbox-next’).addEventListener(‘click’, (e) => { e.stopPropagation(); lbStep(1); });
lb.addEventListener(‘click’, (e) => { if(e.target === lb) closeLightbox(); });
document.addEventListener(‘keydown’, (e) => {
if(!lb.classList.contains(‘open’)) return;
if(e.key === ‘ArrowLeft’) lbStep(-1);
if(e.key === ‘ArrowRight’) lbStep(1);
});
}

// Expose
window.__velo = { openModal, closeModal };
})();
