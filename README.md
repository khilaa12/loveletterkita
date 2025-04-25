# loveletterkita
love letter

import { useState } from 'react';
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Textarea } from "@/components/ui/textarea";

export default function LoveLetter() {
  const [letters, setLetters] = useState([]);
  const [author, setAuthor] = useState("");
  const [content, setContent] = useState("");
  const [password, setPassword] = useState("");
  const [authenticated, setAuthenticated] = useState(false);

  const handleLogin = () => {
    if (password === "sayang123") {
      setAuthenticated(true);
    } else {
      alert("Password salah! Coba lagi ya.");
    }
  };

  const handleSubmit = () => {
    if (author.trim() && content.trim()) {
      const newLetter = {
        author,
        content,
        date: new Date().toLocaleString()
      };
      setLetters([newLetter, ...letters]);
      setAuthor("");
      setContent("");
    }
  };

  if (!authenticated) {
    return (
      <div className="min-h-screen bg-blue-100 flex flex-col items-center justify-center px-4">
        <Card className="w-full max-w-sm bg-white shadow-md rounded-2xl p-6">
          <CardContent className="flex flex-col gap-4">
            <h2 className="text-xl font-semibold">Masukkan Password</h2>
            <Input
              type="password"
              placeholder="Password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
            <Button onClick={handleLogin} className="bg-blue-500 hover:bg-blue-600 text-white">
              Masuk
            </Button>
          </CardContent>
        </Card>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-blue-100 flex flex-col items-center py-10 px-4">
      <h1 className="text-3xl font-bold mb-6">Love Letter Digital</h1>
      <Card className="w-full max-w-md bg-white shadow-md rounded-2xl p-4">
        <CardContent className="flex flex-col gap-4">
          <Input
            placeholder="Namamu atau inisial"
            value={author}
            onChange={(e) => setAuthor(e.target.value)}
          />
          <Textarea
            placeholder="Tulis surat cintamu di sini..."
            value={content}
            onChange={(e) => setContent(e.target.value)}
            rows={5}
          />
          <Button onClick={handleSubmit} className="bg-blue-500 hover:bg-blue-600 text-white">
            Kirim Surat
          </Button>
        </CardContent>
      </Card>

      <div className="w-full max-w-md mt-8 space-y-4">
        {letters.map((letter, index) => (
          <Card key={index} className="bg-white shadow rounded-xl p-4">
            <p className="text-sm text-gray-600 mb-1">{letter.date} dari <strong>{letter.author}</strong></p>
            <p>{letter.content}</p>
          </Card>
        ))}
      </div>
    </div>
  );
}
