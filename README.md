<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Festu</title>
  <link rel="icon" type="image/png" href="festu-logo.png" />
  <link rel="apple-touch-icon" href="festu-logo.png" />
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #eef5f0;
      margin: 0;
      padding: 16px;
      color: #1b2a1e;
    }
    .container {
      max-width: 540px;
      margin: auto;
    }
    .header {
      background: linear-gradient(135deg, #15803d, #16a34a);
      color: #ffffff;
      padding: 12px 16px;
      border-radius: 12px;
      margin-bottom: 14px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 6px rgba(21, 128, 61, 0.25);
    }
    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 22px;
      font-weight: bold;
    }
    .brand img {
      width: 38px;
      height: 38px;
      border-radius: 10px;
      background: #ffffff;
      object-fit: cover;
    }
    .box, .post {
      background: #ffffff;
      padding: 14px;
      border-radius: 12px;
      margin-bottom: 12px;
      box-shadow: 0 1px 4px rgba(0, 0, 0, 0.08);
    }
    input, textarea {
      width: 100%;
      box-sizing: border-box;
      padding: 10px;
      margin-bottom: 10px;
      border: 1px solid #cbd5e1;
      border-radius: 8px;
      font-size: 15px;
    }
    button {
      background: #16a34a;
      color: #ffffff;
      border: none;
      padding: 8px 13px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
      margin-right: 6px;
      margin-bottom: 6px;
    }
    button:hover {
      opacity: 0.94;
    }
    .logout-btn {
      background: #ffffff;
      color: #15803d;
      font-weight: bold;
      padding: 6px 12px;
      margin: 0;
    }
    .follow-btn {
      background: #16a34a;
      color: #ffffff;
      font-weight: bold;
      padding: 5px 10px;
      font-size: 12px;
      margin: 0;
    }
    .unfollow-btn {
      background: #e2e8f0;
      color: #1e293b;
      font-weight: bold;
      padding: 5px 10px;
      font-size: 12px;
      margin: 0;
    }
    .like-btn {
      background: #dcfce7;
      color: #15803d;
      font-weight: bold;
    }
    .share-btn {
      background: #e0f2fe;
      color: #0369a1;
      font-weight: bold;
    }
    .del-btn {
      background: #fee2e2;
      color: #b91c1c;
      font-weight: bold;
    }
    .mini-del-btn {
      background: #fee2e2;
      color: #b91c1c;
      font-size: 11px;
      padding: 3px 7px;
      border-radius: 6px;
      margin-left: 6px;
    }
    .rules-box {
      background: #f0fdf4;
      border: 1px solid #bbf7d0;
      color: #14532d;
      padding: 10px 12px;
      border-radius: 10px;
      font-size: 12.5px;
      margin-bottom: 12px;
    }
    .tabs, .sub-filters {
      display: flex;
      gap: 8px;
      margin-bottom: 12px;
    }
    .tab-btn {
      flex: 1;
      background: #ffffff;
      color: #15803d;
      border: 1px solid #16a34a;
      font-weight: bold;
      margin: 0;
    }
    .tab-btn.active {
      background: #16a34a;
      color: #ffffff;
    }
    .filter-btn {
      background: #ffffff;
      color: #15803d;
      border: 1px solid #86efac;
      font-size: 12.5px;
      padding: 6px 10px;
      margin: 0;
    }
    .filter-btn.active {
      background: #dcfce7;
      border-color: #16a34a;
      font-weight: bold;
    }
    .post-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
    }
    .post-video {
      width: 100%;
      max-height: 360px;
      border-radius: 10px;
      margin-top: 8px;
      background: #000000;
    }
    .actions {
      margin-top: 10px;
    }
    .author {
      font-weight: bold;
      margin-bottom: 2px;
    }
    .meta {
      font-size: 12px;
      color: #64748b;
      margin-bottom: 8px;
    }
    .status {
      font-size: 13px;
      color: #334155;
      margin-bottom: 10px;
    }
    .comments-box {
      background: #f8fafc;
      padding: 10px;
      border-radius: 8px;
      margin-top: 10px;
    }
    .comment-item {
      font-size: 13px;
      padding: 5px 0;
      border-bottom: 1px solid #e2e8f0;
    }
    .comment-item:last-child {
      border-bottom: none;
    }
    .chat-list {
      max-height: 280px;
      overflow-y: auto;
      background: #f8fafc;
      padding: 10px;
      border-radius: 8px;
      margin-bottom: 10px;
    }
    .chat-msg {
      background: #ffffff;
      padding: 8px 10px;
      border-radius: 8px;
      margin-bottom: 8px;
      border: 1px solid #e2e8f0;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- हेडर + लोगो + लॉग-आउट -->
    <div class="header">
      <div class="brand">
        <img src="festu-logo.png" alt="Festu Logo" />
        <span>Festu</span>
      </div>
      <button id="logoutBtn" class="logout-btn hidden" onclick="logoutUser()">लॉग-आउट</button>
    </div>

    <!-- लॉग-इन / रजिस्टर बॉक्स -->
    <div id="authBox" class="box">
      <div class="status">Festu इस्तेमाल करने के लिए लॉग-इन करें या नया अकाउंट बनाएँ</div>
      <input id="emailInput" type="email" placeholder="ईमेल लिखें (जैसे name@example.com)" />
      <input id="passwordInput" type="password" placeholder="पासवर्ड लिखें (कम से कम 6 अक्षर)" />
      <button onclick="loginUser()">लॉग-इन</button>
      <button onclick="signupUser()" style="background:#0f766e;">नया अकाउंट बनाएँ</button>
      <div id="authStatus" class="status"></div>
    </div>

    <!-- लॉग-इन के बाद मुख्य ऐप हिस्सा -->
    <div id="appSection" class="hidden">
      <div id="userInfo" class="meta"></div>
      <div id="followStats" class="meta">फ़ॉलोइंग: 0 | फ़ॉलोअर्स: 0</div>

      <!-- सख़्त नियम बोर्ड -->
      <div class="rules-box">
        <strong>Festu के सख़्त नियम:</strong><br/>
        • गाली-गलौज, धमकी, अश्लील या आपत्तिजनक शब्द/वीडियो मना हैं।<br/>
        • वीडियो अधिकतम <strong>60 सेकंड (1 मिनट)</strong> और <strong>25 MB</strong> तक का ही डालें।<br/>
        • नियम तोड़ने वाली पोस्ट, कमेंट या चैट एडमिन द्वारा तुरंत हटाई जा सकती है।
      </div>

      <input id="displayNameInput" type="text" placeholder="आपका नाम (जो पोस्ट, चैट और फ़ॉलो में दिखेगा)..." />

      <div class="tabs">
        <button id="tabFeedBtn" class="tab-btn active" onclick="switchTab('feed')">पोस्ट फ़ीड</button>
        <button id="tabChatBtn" class="tab-btn" onclick="switchTab('chat')">आपस में चैट</button>
      </div>

      <!-- फ़ीड सेक्शन -->
      <div id="feedSection">
        <div class="box">
          <textarea id="postText" rows="3" placeholder="Festu पर क्या शेयर करना चाहते हैं? (वैकल्पिक यदि वीडियो डाल रहे हैं)"></textarea>
          <div class="meta">1 मिनट (60 सेकंड) तक का वीडियो चुनें (अधिकतम 25 MB):</div>
          <input id="videoInput" type="file" accept="video/mp4,video/webm,video/quicktime,video/*" onchange="handleVideoSelect()" />
          <div id="videoInfo" class="meta"></div>
          <button id="publishBtn" onclick="addPost()">पोस्ट करें</button>
          <div id="uploadStatus" class="status"></div>
        </div>

        <div class="sub-filters">
          <button id="filterAllBtn" class="filter-btn active" onclick="setFeedFilter('all')">सभी पोस्ट</button>
          <button id="filterFollowingBtn" class="filter-btn" onclick="setFeedFilter('following')">केवल फ़ॉलो किए हुए लोग</button>
        </div>

        <div id="feed"></div>
      </div>

      <!-- आपस में बात करने का चैट सेक्शन -->
      <div id="chatSection" class="hidden">
        <div class="box">
          <div class="author">Festu कम्युनिटी चैट (सभी सदस्य यहाँ बात कर सकते हैं)</div>
          <div id="chatList" class="chat-list"></div>
          <input id="chatInput" type="text" placeholder="मैसेज लिखें..." />
          <button onclick="sendChatMessage()">भेजें</button>
        </div>
      </div>
    </div>
  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import {
      getAuth,
      signInWithEmailAndPassword,
      createUserWithEmailAndPassword,
      signOut,
      onAuthStateChanged
    } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
    import {
      getFirestore,
      collection,
      addDoc,
      setDoc,
      onSnapshot,
      query,
      orderBy,
      serverTimestamp,
      doc,
      updateDoc,
      deleteDoc,
      increment
    } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
    import {
      getStorage,
      ref,
      uploadBytes,
      getDownloadURL
    } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-storage.js";

    // अपना Firebase Config यहाँ भरें:
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    // यहाँ अपना एडमिन ईमेल लिखें:
    const ADMIN_EMAIL = "YOUR_ADMIN_EMAIL@example.com";

    // सख़्त नियम: रोके जाने वाले शब्द
    const BLOCKED_WORDS = [
      "chutiya", "madarchod", "bhosdike", "gaandu", "randi",
      "bc", "mc", "abuse", "scam", "fraud", "kill", "rape"
    ];

    const MAX_VIDEO_SECONDS = 60;
    const MAX_VIDEO_BYTES = 25 * 1024 * 1024; // 25 MB

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const storage = getStorage(app);

    const postsRef = collection(db, "festu_posts");
    const chatRef = collection(db, "festu_chat");
    const followsRef = collection(db, "festu_follows");

    let currentUser = null;
    let latestPosts = [];
    let latestChats = [];
    let commentsByPost = {};
    let allFollowDocs = [];
    let feedFilter = "all";
    let lastActionTime = 0;
    let selectedVideoFile = null;

    const authBox = document.getElementById("authBox");
    const appSection = document.getElementById("appSection");
    const logoutBtn = document.getElementById("logoutBtn");
    const authStatus = document.getElementById("authStatus");
    const userInfo = document.getElementById("userInfo");
    const followStats = document.getElementById("followStats");
    const videoInfo = document.getElementById("videoInfo");
    const uploadStatus = document.getElementById("uploadStatus");

    function isAdmin() {
      return !!(currentUser && currentUser.email &&
        currentUser.email.toLowerCase() === ADMIN_EMAIL.toLowerCase());
    }

    function checkStrictRules(text, maxLen, allowEmptyText = false) {
      const clean = text.trim();
      if (!clean && !allowEmptyText) return "खाली संदेश या पोस्ट नहीं भेजी जा सकती।";
      if (clean.length > maxLen) return `अधिकतम ${maxLen} अक्षरों तक ही लिखें।`;

      const now = Date.now();
      if (!isAdmin() && now - lastActionTime < 5000) {
        return "सख़्त नियम: कृपया 5 सेकंड रुककर फिर पोस्ट या मैसेज भेजें।";
      }

      if (!isAdmin() && /(https?:\/\/|www\.|\.com\b|\.in\b|\.xyz\b)/i.test(clean)) {
        return "सख़्त नियम: पोस्ट या चैट में बाहरी लिंक डालना मना है।";
      }

      if (/(.)\1{7,}/i.test(clean)) {
        return "सख़्त नियम: एक ही अक्षर को बार-बार दोहराना स्पैम माना जाता है।";
      }

      const lower = clean.toLowerCase();
      for (const word of BLOCKED_WORDS) {
        if (lower.includes(word)) {
          return "सख़्त नियम: आपत्तिजनक या प्रतिबंधित शब्द इस्तेमाल नहीं कर सकते।";
        }
      }
      return null;
    }

    function getVideoDurationSeconds(file) {
      return new Promise((resolve, reject) => {
        const videoEl = document.createElement("video");
        videoEl.preload = "metadata";
        const objectUrl = URL.createObjectURL(file);

        videoEl.onloadedmetadata = () => {
          URL.revokeObjectURL(objectUrl);
          resolve(Number(videoEl.duration || 0));
        };
        videoEl.onerror = () => {
          URL.revokeObjectURL(objectUrl);
          reject(new Error("वीडियो की अवधि नहीं पढ़ी जा सकी।"));
        };
        videoEl.src = objectUrl;
      });
    }

    window.handleVideoSelect = async function () {
      const input = document.getElementById("videoInput");
      const file = input.files && input.files[0];
      selectedVideoFile = null;
      videoInfo.textContent = "";

      if (!file) return;

      if (!file.type.startsWith("video/")) {
        alert("कृपया केवल वीडियो फ़ाइल चुनें।");
        input.value = "";
        return;
      }

      if (file.size > MAX_VIDEO_BYTES) {
        alert("वीडियो 25 MB से बड़ा नहीं होना चाहिए।");
        input.value = "";
        return;
      }

      try {
        const duration = await getVideoDurationSeconds(file);
        if (duration > MAX_VIDEO_SECONDS) {
          alert(`वीडियो 1 मिनट (${MAX_VIDEO_SECONDS} सेकंड) से लंबा है। कृपया 60 सेकंड या उससे छोटा वीडियो चुनें।`);
          input.value = "";
          return;
        }
        selectedVideoFile = file;
        videoInfo.textContent = `चुना गया वीडियो: ${file.name} (${Math.round(duration)} सेकंड)`;
      } catch (err) {
        alert(err.message);
        input.value = "";
      }
    };

    window.switchTab = function (tab) {
      const feedSec = document.getElementById("feedSection");
      const chatSec = document.getElementById("chatSection");
      const tabFeedBtn = document.getElementById("tabFeedBtn");
      const tabChatBtn = document.getElementById("tabChatBtn");

      if (tab === "chat") {
        feedSec.classList.add("hidden");
        chatSec.classList.remove("hidden");
        tabChatBtn.classList.add("active");
        tabFeedBtn.classList.remove("active");
      } else {
        chatSec.classList.add("hidden");
        feedSec.classList.remove("hidden");
        tabFeedBtn.classList.add("active");
        tabChatBtn.classList.remove("active");
      }
    };

    window.setFeedFilter = function (mode) {
      feedFilter = mode;
      document.getElementById("filterAllBtn").classList.toggle("active", mode === "all");
      document.getElementById("filterFollowingBtn").classList.toggle("active", mode === "following");
      renderFeed();
    };

    window.loginUser = async function () {
      const email = document.getElementById("emailInput").value.trim();
      const password = document.getElementById("passwordInput").value.trim();
      if (!email || !password) {
        authStatus.textContent = "कृपया ईमेल और पासवर्ड दोनों लिखें।";
        return;
      }
      try {
        authStatus.textContent = "लॉग-इन हो रहा है...";
        await signInWithEmailAndPassword(auth, email, password);
        authStatus.textContent = "लॉग-इन सफल हुआ!";
      } catch (err) {
        authStatus.textContent = "लॉग-इन नहीं हो सका: " + err.message;
      }
    };

    window.signupUser = async function () {
      const email = document.getElementById("emailInput").value.trim();
      const password = document.getElementById("passwordInput").value.trim();
      if (!email || password.length < 6) {
        authStatus.textContent = "ईमेल डालें और पासवर्ड कम से कम 6 अक्षरों का रखें।";
        return;
      }
      try {
        authStatus.textContent = "अकाउंट बनाया जा रहा है...";
        await createUserWithEmailAndPassword(auth, email, password);
        authStatus.textContent = "अकाउंट बन गया और आप लॉग-इन हो गए!";
      } catch (err) {
        authStatus.textContent = "अकाउंट बनाने में समस्या: " + err.message;
      }
    };

    window.logoutUser = async function () {
      try {
        await signOut(auth);
        authStatus.textContent = "आप लॉग-आउट हो चुके हैं।";
      } catch (err) {
        alert("लॉग-आउट में समस्या: " + err.message);
      }
    };

    onAuthStateChanged(auth, (user) => {
      currentUser = user;
      if (user) {
        authBox.classList.add("hidden");
        appSection.classList.remove("hidden");
        logoutBtn.classList.remove("hidden");
        userInfo.textContent = "लॉग-इन: " + (user.email || "") + (isAdmin() ? " • [ADMIN]" : "");
        listenToPosts();
        listenToChats();
        listenToFollows();
      } else {
        authBox.classList.remove("hidden");
        appSection.classList.add("hidden");
        logoutBtn.classList.add("hidden");
        userInfo.textContent = "";
      }
    });

    function getUserName() {
      const val = document.getElementById("displayNameInput").value.trim();
      if (val) return val.slice(0, 40);
      if (currentUser && currentUser.email) return currentUser.email.split("@")[0];
      return "Festu User";
    }

    function listenToFollows() {
      onSnapshot(followsRef, (snapshot) => {
        allFollowDocs = [];
        snapshot.forEach((d) => {
          allFollowDocs.push({ id: d.id, ...d.data() });
        });
        updateFollowStats();
        renderFeed();
      });
    }

    function isFollowing(targetUid) {
      if (!currentUser || !targetUid) return false;
      const docId = `${currentUser.uid}_${targetUid}`;
      return allFollowDocs.some((item) => item.id === docId);
    }

    function updateFollowStats() {
      if (!currentUser) return;
      const followingCount = allFollowDocs.filter((x) => x.followerUid === currentUser.uid).length;
      const followersCount = allFollowDocs.filter((x) => x.followingUid === currentUser.uid).length;
      followStats.textContent = `फ़ॉलोइंग: ${followingCount} | फ़ॉलोअर्स: ${followersCount}`;
    }

    window.toggleFollow = async function (targetUid, targetName) {
      if (!currentUser || !targetUid || targetUid === currentUser.uid) return;
      const edgeId = `${currentUser.uid}_${targetUid}`;
      const edgeRef = doc(db, "festu_follows", edgeId);

      if (isFollowing(targetUid)) {
        await deleteDoc(edgeRef);
      } else {
        await setDoc(edgeRef, {
          followerUid: currentUser.uid,
          followerName: getUserName(),
          followingUid: targetUid,
          followingName: targetName || "Festu User",
          createdAt: serverTimestamp()
        });
      }
    };

    function listenToPosts() {
      const q = query(postsRef, orderBy("createdAt", "desc"));
      onSnapshot(q, (snapshot) => {
        latestPosts = [];
        snapshot.forEach((docSnap) => {
          const postId = docSnap.id;
          latestPosts.push({ id: postId, ...docSnap.data() });
          listenToComments(postId);
        });
        renderFeed();
      });
    }

    function listenToComments(postId) {
      const cRef = collection(db, "festu_posts", postId, "comments");
      const q = query(cRef, orderBy("createdAt", "asc"));
      onSnapshot(q, (snapshot) => {
        commentsByPost[postId] = [];
        snapshot.forEach((cSnap) => {
          commentsByPost[postId].push({ id: cSnap.id, ...cSnap.data() });
        });
        renderFeed();
      });
    }

    function renderFeed() {
      const feed = document.getElementById("feed");
      if (!feed) return;
      feed.innerHTML = "";

      const followingUids = currentUser
        ? allFollowDocs.filter((x) => x.followerUid === currentUser.uid).map((x) => x.followingUid)
        : [];

      const visiblePosts = feedFilter === "following"
        ? latestPosts.filter((p) => followingUids.includes(p.ownerUid))
        : latestPosts;

      if (visiblePosts.length === 0) {
        feed.innerHTML = `<div class="box meta">${feedFilter === "following"
          ? "आपने अभी किसी को फ़ॉलो नहीं किया है या फ़ॉलो किए गए लोगों की कोई पोस्ट नहीं है।"
          : "अभी कोई पोस्ट नहीं है।"}</div>`;
        return;
      }

      visiblePosts.forEach((p) => {
        const isSelf = currentUser && p.ownerUid === currentUser.uid;
        const alreadyFollowed = isFollowing(p.ownerUid);
        const followBtnHtml = (!isSelf && p.ownerUid)
          ? `<button class="${alreadyFollowed ? "unfollow-btn" : "follow-btn"}" onclick="toggleFollow('${p.ownerUid}', '${escapeJs(p.name || "Festu User")}')">${alreadyFollowed ? "✓ अनफ़ॉलो" : "+ फ़ॉलो करें"}</button>`
          : "";

        const canDeletePost = currentUser && (isSelf || isAdmin());
        const deleteBtn = canDeletePost
          ? `<button class="del-btn" onclick="deletePost('${p.id}')">🗑️ ${isAdmin() && !isSelf ? "एडमिन हटाएँ" : "हटाएँ"}</button>`
          : "";

        const videoHtml = p.videoUrl
          ? `<video class="post-video" src="${escapeHtml(p.videoUrl)}" controls playsinline preload="metadata"></video>`
          : "";

        const postComments = commentsByPost[p.id] || [];
        const commentsHtml = postComments.map((c) => {
          const canDeleteComment = currentUser && (c.ownerUid === currentUser.uid || isAdmin());
          const delCommentBtn = canDeleteComment
            ? `<button class="mini-del-btn" onclick="deleteComment('${p.id}', '${c.id}')">हटाएँ</button>`
            : "";
          return `
            <div class="comment-item">
              <strong>${escapeHtml(c.authorName || "User")}:</strong> ${escapeHtml(c.text || "")}
              ${delCommentBtn}
            </div>
          `;
        }).join("");

        feed.innerHTML += `
          <div class="post">
            <div class="post-top">
              <div>
                <div class="author">${escapeHtml(p.name || "Festu User")}</div>
                <div class="meta">${escapeHtml(p.email || "")}</div>
              </div>
              ${followBtnHtml}
            </div>
            ${p.text ? `<div>${escapeHtml(p.text)}</div>` : ""}
            ${videoHtml}
            <div class="actions">
              <button class="like-btn" onclick="likePost('${p.id}')">👍 लाइक (${p.likes || 0})</button>
              <button class="share-btn" onclick="sharePost('${p.id}')">↗️ शेयर</button>
              ${deleteBtn}
            </div>
            <div class="comments-box">
              ${commentsHtml || '<div class="meta">अभी कोई कमेंट नहीं है</div>'}
              <input id="commentInput-${p.id}" type="text" placeholder="कमेंट लिखें..." style="margin-top:8px; margin-bottom:6px;" />
              <button onclick="addComment('${p.id}')">कमेंट करें</button>
            </div>
          </div>
        `;
      });
    }

    window.addPost = async function () {
      if (!currentUser) return;
      const textInput = document.getElementById("postText");
      const videoInput = document.getElementById("videoInput");
      const publishBtn = document.getElementById("publishBtn");

      const hasVideo = !!selectedVideoFile;
      const ruleError = checkStrictRules(textInput.value, 1000, hasVideo);
      if (ruleError) {
        alert(ruleError);
        return;
      }

      if (hasVideo) {
        if (selectedVideoFile.size > MAX_VIDEO_BYTES) {
          alert("वीडियो 25 MB से बड़ा नहीं होना चाहिए।");
          return;
        }
        try {
          const duration = await getVideoDurationSeconds(selectedVideoFile);
          if (duration > MAX_VIDEO_SECONDS) {
            alert(`वीडियो 1 मिनट (${MAX_VIDEO_SECONDS} सेकंड) से लंबा है।`);
            return;
          }
        } catch (err) {
          alert(err.message);
          return;
        }
      }

      publishBtn.disabled = true;
      lastActionTime = Date.now();

      try {
        let videoUrl = "";
        if (hasVideo) {
          uploadStatus.textContent = "वीडियो अपलोड हो रहा है...";
          const safeName = `${Date.now()}_${selectedVideoFile.name.replace(/[^a-zA-Z0-9._-]/g, "_")}`;
          const storageRef = ref(storage, `festu_videos/${currentUser.uid}/${safeName}`);
          await uploadBytes(storageRef, selectedVideoFile);
          videoUrl = await getDownloadURL(storageRef);
        }

        const cleanText = textInput.value.trim();
        textInput.value = "";
        videoInput.value = "";
        selectedVideoFile = null;
        videoInfo.textContent = "";
        uploadStatus.textContent = "";

        await addDoc(postsRef, {
          name: getUserName(),
          email: currentUser.email || "",
          ownerUid: currentUser.uid,
          text: cleanText,
          videoUrl,
          likes: 0,
          createdAt: serverTimestamp()
        });
      } catch (err) {
        uploadStatus.textContent = "पोस्ट/वीडियो डालने में समस्या: " + err.message;
      } finally {
        publishBtn.disabled = false;
      }
    };

    window.likePost = async function (postId) {
      if (!currentUser) return;
      await updateDoc(doc(db, "festu_posts", postId), {
        likes: increment(1)
      });
    };

    window.sharePost = async function (postId) {
      const target = latestPosts.find((item) => item.id === postId);
      const shareText = target
        ? `Festu पोस्ट (${target.name}): ${target.text || "वीडियो पोस्ट"}\nलिंक: ${window.location.href}`
        : `Festu देखें: ${window.location.href}`;

      if (navigator.share) {
        try {
          await navigator.share({ title: "Festu", text: shareText, url: window.location.href });
          return;
        } catch (_) {}
      }
      if (navigator.clipboard) {
        await navigator.clipboard.writeText(shareText);
        alert("पोस्ट और लिंक कॉपी हो गया है!");
      }
    };

    window.addComment = async function (postId) {
      if (!currentUser) return;
      const input = document.getElementById("commentInput-" + postId);
      if (!input) return;
      const ruleError = checkStrictRules(input.value, 400, false);
      if (ruleError) {
        alert(ruleError);
        return;
      }

      const cleanText = input.value.trim();
      lastActionTime = Date.now();
      input.value = "";
      const cRef = collection(db, "festu_posts", postId, "comments");
      await addDoc(cRef, {
        authorName: getUserName(),
        ownerUid: currentUser.uid,
        text: cleanText,
        createdAt: serverTimestamp()
      });
    };

    window.deletePost = async function (postId) {
      if (!currentUser) return;
      const target = latestPosts.find((item) => item.id === postId);
      if (!target || (target.ownerUid !== currentUser.uid && !isAdmin())) {
        alert("आप केवल अपनी पोस्ट हटा सकते हैं या एडमिन ही गलत पोस्ट हटा सकता है।");
        return;
      }
      if (!confirm("क्या आप वाकई यह पोस्ट हटाना चाहते हैं?")) return;
      await deleteDoc(doc(db, "festu_posts", postId));
    };

    window.deleteComment = async function (postId, commentId) {
      if (!currentUser) return;
      const list = commentsByPost[postId] || [];
      const target = list.find((c) => c.id === commentId);
      if (!target || (target.ownerUid !== currentUser.uid && !isAdmin())) {
        alert("इस कमेंट को हटाने की अनुमति नहीं है।");
        return;
      }
      if (!confirm("क्या यह कमेंट हटाना है?")) return;
      await deleteDoc(doc(db, "festu_posts", postId, "comments", commentId));
    };

    function listenToChats() {
      const q = query(chatRef, orderBy("createdAt", "asc"));
      onSnapshot(q, (snapshot) => {
        latestChats = [];
        snapshot.forEach((cSnap) => {
          latestChats.push({ id: cSnap.id, ...cSnap.data() });
        });
        renderChats();
      });
    }

    function renderChats() {
      const chatList = document.getElementById("chatList");
      if (!chatList) return;
      chatList.innerHTML = latestChats.map((m) => {
        const canDeleteChat = currentUser && (m.ownerUid === currentUser.uid || isAdmin());
        const delChatBtn = canDeleteChat
          ? `<button class="mini-del-btn" onclick="deleteChat('${m.id}')">हटाएँ</button>`
          : "";
        return `
          <div class="chat-msg">
            <div class="author">${escapeHtml(m.senderName || "Festu User")} ${delChatBtn}</div>
            <div>${escapeHtml(m.text || "")}</div>
          </div>
        `;
      }).join("") || '<div class="meta">अभी कोई चैट मैसेज नहीं है। बातचीत शुरू करें!</div>';
      chatList.scrollTop = chatList.scrollHeight;
    }

    window.sendChatMessage = async function () {
      if (!currentUser) return;
      const input = document.getElementById("chatInput");
      const ruleError = checkStrictRules(input.value, 500, false);
      if (ruleError) {
        alert(ruleError);
        return;
      }

      const cleanText = input.value.trim();
      lastActionTime = Date.now();
      input.value = "";
      await addDoc(chatRef, {
        senderName: getUserName(),
        ownerUid: currentUser.uid,
        text: cleanText,
        createdAt: serverTimestamp()
      });
    };

    window.deleteChat = async function (msgId) {
      if (!currentUser) return;
      const target = latestChats.find((m) => m.id === msgId);
      if (!target || (target.ownerUid !== currentUser.uid && !isAdmin())) {
        alert("इस मैसेज को हटाने की अनुमति नहीं है।");
        return;
      }
      if (!confirm("क्या यह चैट मैसेज हटाना है?")) return;
      await deleteDoc(doc(db, "festu_chat", msgId));
    };

    function escapeHtml(str) {
      return String(str).replace(/[&<>"']/g, (m) => ({
        "&": "&amp;",
        "<": "&lt;",
        ">": "&gt;",
        '"': "&quot;",
        "'": "&#39;"
      }[m]));
    }

    function escapeJs(str) {
      return String(str).replace(/\\/g, "\\\\").replace(/'/g, "\\'");
    }
  </script>
</body>
</html>
