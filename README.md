# nexora-design-studio
NEXORA – Free AI Design Studio

<!-- NEXORA Besucherzähler -->
<style>
  .nexora-counter {
    margin: 30px auto;
    padding: 22px;
    max-width: 320px;
    text-align: center;
    background: #151020;
    border: 1px solid #8b5cf6;
    border-radius: 16px;
    color: white;
    font-family: Arial, sans-serif;
  }

  .nexora-counter h2 {
    color: #c084fc;
    font-size: 18px;
  }

  .nexora-counter strong {
    display: block;
    color: #c084fc;
    font-size: 38px;
    margin-top: 10px;
  }
</style>

<div class="nexora-counter">
  <h2>NEXORA · BESUCHER</h2>
  <strong id="nexora-visits">Lädt...</strong>
  <small>Besuche insgesamt</small>
</div>

<script>
(async function () {
  const key = "nexora-home-2026-11";
  const base = "https://countapi.mileshilliard.com/api/v1";
  const output = document.getElementById("nexora-visits");

  try {
    const alreadyCounted = sessionStorage.getItem("nexora-counted");

    const endpoint = alreadyCounted
      ? `${base}/get/${key}`
      : `${base}/hit/${key}`;

    const response = await fetch(endpoint, {
      cache: "no-store"
    });

    if (!response.ok) throw new Error("Counter unavailable");

    const data = await response.json();

    if (!alreadyCounted) {
      sessionStorage.setItem("nexora-counted", "yes");
    }

    output.textContent = Number(data.value).toLocaleString("de-DE");
  } catch (error) {
    output.textContent = "Nicht verfügbar";
  }
})();
</script>
