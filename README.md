# Savage-aiasync function sendMessage() {
  const q = input.value.trim();
  if (!q) return;

  add(q, "user");
  input.value = "";

  try {
    const response = await fetch("/api/chat", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        message: q
      })
    });

    const data = await response.json();

    if (!response.ok) {
      throw new Error(data.error || "Request failed");
    }

    add(data.reply, "ai");

  } catch (error) {
    console.error(error);
    add("Sorry, Savage AI could not respond right now. Please try again.", "ai");
  }
}
