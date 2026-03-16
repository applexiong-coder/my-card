# <!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <title>个人名片 - apple不好惹</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    /* 全局重置与基础设置 */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans SC", sans-serif;
      /* 浅蓝色背景（由浅蓝到更浅的渐变） */
      background: linear-gradient(135deg, #bfdbfe, #e0f2fe);
      color: #111827;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 16px;
    }

    /* 名片卡片容器 */
    .card {
      background: #ffffff;
      border-radius: 18px;
      padding: 24px 22px 22px;
      max-width: 380px;
      width: 100%;
      box-shadow:
        0 16px 40px rgba(15, 23, 42, 0.25),
        0 0 0 1px rgba(148, 163, 184, 0.2);
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    /* 卡片内的轻微光效 */
    .card::before {
      content: "";
      position: absolute;
      inset: -40%;
      background: radial-gradient(circle at top left, rgba(59, 130, 246, 0.18), transparent 55%);
      opacity: 0.9;
      pointer-events: none;
    }

    .card-inner {
      position: relative;
      z-index: 1;
    }

    /* 头像区域 */
    .avatar-wrapper {
      margin-bottom: 16px;
    }

    .avatar {
      width: 96px;
      height: 96px;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid rgba(59, 130, 246, 0.85);
      box-shadow: 0 10px 25px rgba(15, 23, 42, 0.25);
      background: #e5e7eb;
    }

    /* 名字与头衔 */
    .name {
      font-size: 1.6rem;
      font-weight: 700;
      color: #111827;
      margin-bottom: 4px;
    }

    .title {
      font-size: 0.9rem;
      color: #6b7280;
      margin-bottom: 14px;
      letter-spacing: 0.03em;
    }

    /* 小分割线 */
    .divider {
      width: 42px;
      height: 3px;
      border-radius: 999px;
      background: linear-gradient(90deg, #3b82f6, #8b5cf6);
      margin: 0 auto 16px;
    }

    /* 简介文字 */
    .bio {
      font-size: 0.9rem;
      color: #4b5563;
      line-height: 1.6;
      margin-bottom: 18px;
    }

    /* 联系方式模块 */
    .contact {
      text-align: left;
      font-size: 0.9rem;
      color: #374151;
      background: #f3f4f6;
      padding: 10px 12px;
      border-radius: 12px;
      margin-bottom: 10px;
    }

    .contact-row {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 6px;
      word-break: break-all;
    }

    .contact-row:last-child {
      margin-bottom: 0;
    }

    .contact-label {
      font-weight: 600;
      color: #6b7280;
      min-width: 48px;
    }

    .contact-value a {
      color: #2563eb;
      text-decoration: none;
    }

    .contact-value a:hover {
      text-decoration: underline;
    }

    /* 兴趣爱好 & 擅长技能 */
    .info-section {
      text-align: left;
      background: #eff6ff;
      border-radius: 12px;
      padding: 10px 12px;
      font-size: 0.88rem;
      color: #1f2937;
      margin-bottom: 12px;
      border: 1px solid rgba(129, 140, 248, 0.35);
    }

    .info-block + .info-block {
      margin-top: 8px;
    }

    .info-title {
      font-weight: 600;
      color: #1d4ed8;
      margin-bottom: 4px;
      font-size: 0.86rem;
    }

    .info-text {
      color: #374151;
      line-height: 1.5;
    }

    /* 大图展示区域，让照片以卡片宽度展示 */
    .photo-full {
      margin-bottom: 12px;
      border-radius: 14px;
      overflow: hidden;
      box-shadow: 0 10px 25px rgba(15, 23, 42, 0.18);
    }

    .photo-full img {
      width: 100%;
      display: block;
    }

    /* 底部链接按钮区（GitHub / 个人主页等） */
    .links {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-top: 6px;
      flex-wrap: wrap;
    }

    .btn-link {
      font-size: 0.85rem;
      padding: 7px 14px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.7);
      background: rgba(249, 250, 251, 0.9);
      color: #111827;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: all 0.18s ease-out;
      backdrop-filter: blur(6px);
    }

    .btn-link:hover {
      border-color: #3b82f6;
      color: #1d4ed8;
      box-shadow: 0 8px 18px rgba(37, 99, 235, 0.2);
      transform: translateY(-1px);
      background: #ffffff;
    }

    /* 不可点击的 GitHub 占位按钮 */
    .btn-link.disabled {
      cursor: default;
      opacity: 0.75;
      border-style: dashed;
    }

    .btn-link.disabled:hover {
      border-color: rgba(148, 163, 184, 0.7);
      color: #111827;
      box-shadow: none;
      transform: none;
      background: rgba(249, 250, 251, 0.9);
    }

    .btn-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: #22c55e;
    }

    /* 移动端适配 */
    @media (max-width: 480px) {
      .card {
        padding: 20px 16px 18px;
        border-radius: 16px;
      }

      .name {
        font-size: 1.35rem;
      }

      .bio {
        font-size: 0.88rem;
      }

      .contact,
      .info-section {
        font-size: 0.86rem;
      }

      .btn-link {
        padding: 6px 12px;
      }
    }
  </style>
</head>
<body>
  <!-- 个人名片主卡片 -->
  <main class="card">
    <div class="card-inner">
      <!-- 头像 -->
      <div class="avatar-wrapper">
        <!-- 确保 IMG_7105.JPG 与 index.html 在同一文件夹 -->
        <img
          class="avatar"
          src="IMG_7105.JPG"
          alt="头像"
        />
      </div>

      <!-- 大图展示（使用同一张照片） -->
      <div class="photo-full">
        <img src="IMG_7105.JPG" alt="apple不好惹的照片" />
      </div>

      <!-- 姓名与头衔 -->
      <h1 class="name">apple不好惹</h1>
      <p class="title">前端开发 / 产品爱好者</p>

      <div class="divider"></div>

      <!-- 个人简介 -->
      <p class="bio">
        普通人类，间歇性想退休，持续性在努力，主打一个心态平稳，偶尔发疯。
      </p>

      <!-- 联系方式 -->
      <section class="contact" aria-label="联系方式">
        <div class="contact-row">
          <span class="contact-label">邮箱</span>
          <span class="contact-value">
            <a href="mailto:3847328@qq.com">3847328@qq.com</a>
          </span>
        </div>
        <div class="contact-row">
          <span class="contact-label">手机</span>
          <span class="contact-value">18923885880</span>
        </div>
        <div class="contact-row">
          <span class="contact-label">微信</span>
          <span class="contact-value">pple2710</span>
        </div>
      </section>

      <!-- 兴趣爱好 & 擅长技能 -->
      <section class="info-section" aria-label="个人标签">
        <div class="info-block">
          <div class="info-title">兴趣爱好</div>
          <div class="info-text">
            吃饭、睡觉、抢救自己的精神状态。
          </div>
        </div>
        <div class="info-block">
          <div class="info-title">擅长技能</div>
          <div class="info-text">
            没什么特长，就是擅长把日子过得可盐可甜。
          </div>
        </div>
      </section>

      <!-- 外部链接（GitHub / 个人主页） -->
      <div class="links">
        <!-- GitHub 占位按钮（不可点击） -->
        <a class="btn-link disabled" href="javascript:void(0)">
          <span class="btn-dot"></span>
          <span>GitHub：正在建设中</span>
        </a>

        <!-- 个人主页链接 -->
        <a
          class="btn-link"
          href="https://WWW.就不告诉你就不告诉你就不告诉你.com"
          target="_blank"
          rel="noopener noreferrer"
        >
          <span>个人主页</span>
        </a>
      </div>
    </div>
  </main>
</body>
</html>
