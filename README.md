import React, { useState } from "react";

export default function CineSApp() {
  // ----- ESTADOS PRINCIPAIS -----
  const [screen, setScreen] = useState("home"); // home | player
  const [currentVideo, setCurrentVideo] = useState(null);

  // ----- LISTA DE FILMES -----
  const filmes = [
    {
      id: 1,
      titulo: "Filme 1",
      thumb: "https://via.placeholder.com/300x170?text=Filme+1",
      url: "https://www.w3schools.com/html/mov_bbb.mp4"
    },
    {
      id: 2,
      titulo: "Filme 2",
      thumb: "https://via.placeholder.com/300x170?text=Filme+2",
      url: "https://www.w3schools.com/html/movie.mp4"
    }
  ];

  // ----- ABRIR PLAYER -----
  function openPlayer(video) {
    setCurrentVideo(video);
    setScreen("player");
  }

  // ----- TELA DO PLAYER -----
  if (screen === "player" && currentVideo) {
    return (
      <div style={{ padding: 20, color: "#fff", background: "#111", height: "100vh" }}>
        <h2>{currentVideo.titulo}</h2>

        <video
          src={currentVideo.url}
          style={{ width: "100%", maxHeight: "70vh", borderRadius: "10px" }}
          controls
          autoPlay
        />

        <button
          style={{
            marginTop: 20,
            padding: "10px 20px",
            borderRadius: "10px",
            fontSize: 18,
            cursor: "pointer"
          }}
          onClick={() => setScreen("home")}
        >
          ⬅ Voltar
        </button>
      </div>
    );
  }

  // ----- TELA INICIAL -----
  return (
    <div style={{ padding: 20, color: "#fff", background: "#000", minHeight: "100vh" }}>
      <h1>Cine S 🎬</h1>

      <div style={{ display: "grid", gap: 20 }}>
        {filmes.map((v) => (
          <div
            key={v.id}
            style={{
              background: "#222",
              padding: 15,
              borderRadius: "10px",
              display: "flex",
              gap: 15
            }}
          >
            <img
              src={v.thumb}
              style={{ width: 120, height: 80, borderRadius: 10 }}
            />

            <div>
              <h3>{v.titulo}</h3>

              <button
                style={{
                  marginTop: 10,
                  padding: "8px 16px",
                  borderRadius: "10px",
                  cursor: "pointer",
                  fontSize: 16
                }}
                onClick={() => openPlayer(v)}
              >
                ▶ Assistir
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}
