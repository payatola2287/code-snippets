# WordPress Technical Review Checklist

<details>
  <summary>1. Server & Hosting Layer</summary>
  <ul>
    <li>Verify PHP version (≥ 8.1) and MySQL/MariaDB compatibility.</li>
    <li>Confirm SiteGround caching plugin integration (no duplicate caching layers).</li>
    <li>Check file permissions (<code>wp-config.php</code> locked down, uploads writable).</li>
    <li>Benchmark TTFB (Time to First Byte) via WebPageTest.</li>
    <li>Test staging environment deployment and rollback.</li>
  </ul>
</details>

<details>
  <summary>2. WordPress Core & Plugins</summary>
  <ul>
    <li>Ensure WordPress core is updated.</li>
    <li>Verify <code>wp-config.php</code> constants (debug mode off in production, correct table prefix).</li>
    <li>Update Elementor, Elementor Pro, Ultimate Addons, Dynamic Content for Elementor, and Contact Form 7.</li>
    <li>Audit for redundant functionality (overlapping Elementor addons).</li>
    <li>Test plugin conflicts with SiteGround caching (disable caching temporarily to confirm dynamic widgets and forms work).</li>
  </ul>
</details>

<details>
  <summary>3. Theme & Asset Loading</summary>
  <ul>
    <li>Confirm child theme usage for customizations.</li>
    <li>Validate enqueueing of CSS/JS (no duplicate Elementor assets).</li>
    <li>Test lazy loading for images and background sections.</li>
    <li>Ensure SiteGround caching plugin minifies CSS/JS correctly.</li>
  </ul>
</details>

<details>
  <summary>4. Performance Baseline</summary>
  <ul>
    <li>Core Web Vitals (in correct order):
      <ol>
        <li>Largest Contentful Paint (LCP) – loading speed.</li>
        <li>Interaction to Next Paint (INP) – interactivity.</li>
        <li>Cumulative Layout Shift (CLS) – stability.</li>
      </ol>
    </li>
  </ul>
  <h4>Image Delivery Testing</h4>
  <ul>
    <li>Run Lighthouse → check:
      <ul>
        <li>Serve images in next-gen formats (WebP/AVIF).</li>
        <li>Properly size images (no oversized assets).</li>
        <li>Efficiently encode images (compression).</li>
        <li>Lazy load offscreen images.</li>
      </ul>
    </li>
    <li>Cross-check in DevTools → Network tab (filter by Img):
      <ul>
        <li>File size (KB/MB).</li>
        <li>Format (WebP/AVIF vs JPEG/PNG).</li>
        <li>Cache headers (TTL set by SiteGround plugin).</li>
        <li>Delivery source (CDN vs origin).</li>
      </ul>
    </li>
    <li>Confirm hero/LCP image is optimized and preloaded.</li>
    <li>Validate <code>srcset</code> and <code>sizes</code> attributes for responsive images.</li>
  </ul>
</details>

<details>
  <summary>5. Security</summary>
  <ul>
    <li>Confirm HTTPS enforced site-wide.</li>
    <li>Confirm no mixed content via DevTools → Console tab.</li>
    <li>Validate headers in DevTools → Network tab:
      <ul>
        <li>Strict-Transport-Security (HSTS).</li>
        <li>Content-Security-Policy (CSP).</li>
        <li>X-Frame-Options.</li>
        <li>X-Content-Type-Options: nosniff.</li>
        <li>Referrer-Policy.</li>
      </ul>
    </li>
    <li>Audit user roles in WordPress Admin → Users (least privilege principle).</li>
    <li>Run WPScan (free API mode) for plugin/theme vulnerabilities.</li>
    <li>Use Lighthouse → Best Practices audit for insecure requests and outdated libraries.</li>
  </ul>
</details>

<details>
  <summary>6. On-Page SEO (Indexing Off but Structure Valid)</summary>
  <ul>
    <li>Validate meta titles and descriptions per page in Elementor.</li>
    <li>Check heading hierarchy (H1 → H2 → H3).</li>
    <li>Confirm alt text for all images.</li>
    <li>Validate canonical tags.</li>
    <li>Test schema markup (Organization, Breadcrumbs).</li>
  </ul>
</details>

<details>
  <summary>7. Accessibility</summary>
  <ul>
    <li>Test keyboard navigation for Elementor modals, sliders, and forms.</li>
    <li>Validate color contrast against WCAG 2.1.</li>
    <li>Ensure ARIA roles are applied to dynamic widgets.</li>
  </ul>
</details>

<details>
  <summary>8. Functional Testing</summary>
  <ul>
    <li>Test Contact Form 7 submissions with caching exclusions.</li>
    <li>Validate navigation menus, breadcrumbs, footer links.</li>
    <li>Test Elementor breakpoints (mobile, tablet, desktop).</li>
  </ul>
</details>

<details>
  <summary>9. Monitoring & Logging</summary>
  <ul>
    <li>Enable WP_DEBUG_LOG in staging.</li>
    <li>Confirm Site Kit or GA4 tracking scripts fire correctly.</li>
    <li>Integrate uptime monitoring (Pingdom/UptimeRobot).</li>
    <li>Ensure activity logs for admin actions.</li>
  </ul>
</details>
