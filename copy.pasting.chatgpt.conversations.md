
	function copyChatGPTConversationToLocalStorage() {
	  const chatDiv = document.querySelector("div.flex.flex-col.text-sm")?.parentElement;
	  if (!chatDiv) return console.warn("❌ Chat div not found.");

	  // Grab all actual message articles
	  const articles = chatDiv.querySelectorAll("article.text-token-text-primary");
	  if (!articles.length) return console.warn("⚠️ No messages found in chat.");
	  const serializedArticles = Array.from(articles).map(a => a.outerHTML).join("\n");
	  localStorage.setItem("chatGPTConversation", serializedArticles);
	  
	  console.log("✅ Chat conversation saved to localStorage (full articles).");
	}

	function pasteChatGPTConversationFromLocalStorageAndClear() {
	  const chatFeed = document.querySelector("div.flex.flex-col.text-sm")?.parentElement;
	  if (!chatFeed) return console.warn("❌ Chat feed not found.");

	  const content = localStorage.getItem("chatGPTConversation");
	  if (!content) return console.warn("⚠️ No saved conversation found. Run copy first.");

	  // Remove all existing message articles
	  chatFeed.querySelectorAll("article.text-token-text-primary").forEach(a => a.remove());

	  // Parse saved articles
	  const tempContainer = document.createElement("div");
	  tempContainer.innerHTML = content;

	  // Sort articles by conversation-turn index if present
	  const sortedArticles = Array.from(tempContainer.children).sort((a, b) => {
		const aIndex = parseInt(a.dataset.testid?.replace("conversation-turn-", "") || 0, 10);
		const bIndex = parseInt(b.dataset.testid?.replace("conversation-turn-", "") || 0, 10);
		return aIndex - bIndex;
	  });

	  // Create a container for the whole set
	  const blockContainer = document.createElement("div");
	  sortedArticles.forEach(article => blockContainer.appendChild(article));

	  // Prepend the block to the chatFeed
	  chatFeed.prepend(blockContainer);

	  localStorage.removeItem("chatGPTConversation");
	  console.log("✅ Chat conversation restored at the top (full block).");
	}


