<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Freelance Portfolio Generator</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen flex items-center justify-center p-6">
  <div class="bg-white p-8 rounded-2xl shadow-xl w-full max-w-3xl">
    <h2 class="text-2xl font-bold mb-6 text-center">Freelance Portfolio & CV Generator</h2>
    <div class="space-y-4">
      <input id="name" type="text" placeholder="Your Name" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="title" type="text" placeholder="Your Title (e.g., Web Developer)" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="skills" type="text" placeholder="Your Skills (comma separated)" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="services" type="text" placeholder="Services Offered" class="w-full p-3 border border-gray-300 rounded-xl" />
      <textarea id="experience" placeholder="Experience (1-2 lines)" class="w-full p-3 border border-gray-300 rounded-xl"></textarea>
      <textarea id="education" placeholder="Education (1-2 lines)" class="w-full p-3 border border-gray-300 rounded-xl"></textarea>
      <input id="email" type="text" placeholder="Your Email" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="linkedin" type="text" placeholder="LinkedIn URL" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="jobTitle" type="text" placeholder="Job Title for Cover Letter" class="w-full p-3 border border-gray-300 rounded-xl" />
      <input id="company" type="text" placeholder="Company Name for Cover Letter" class="w-full p-3 border border-gray-300 rounded-xl" />
      <select id="template" class="w-full p-3 border border-gray-300 rounded-xl">
        <option value="classic">Classic Template</option>
        <option value="modern">Modern Template</option>
      </select>
      <button onclick="generatePortfolio()" class="w-full bg-blue-600 text-white p-3 rounded-xl font-semibold">Generate Portfolio</button>
      <button onclick="downloadPortfolio()" class="w-full bg-green-600 text-white p-3 rounded-xl font-semibold">Download HTML</button>
    </div>

    <div id="result" class="mt-8 bg-gray-50 p-6 rounded-xl border border-gray-200"></div>
  </div>

  <script>
    let portfolioHtml = "";

    function generatePortfolio() {
      const name = document.getElementById('name').value;
      const title = document.getElementById('title').value;
      const skills = document.getElementById('skills').value;
      const services = document.getElementById('services').value;
      const experience = document.getElementById('experience').value;
      const education = document.getElementById('education').value;
      const email = document.getElementById('email').value;
      const linkedin = document.getElementById('linkedin').value;
      const jobTitle = document.getElementById('jobTitle').value;
      const company = document.getElementById('company').value;
      const template = document.getElementById('template').value;

      let coverLetter = `
        <h2>Cover Letter</h2>
        <p>Dear Hiring Manager at ${company},</p>
        <p>I am writing to express my interest in the ${jobTitle} position at your company. With my experience in ${skills}, and a proven record of offering ${services}, I am confident in my ability to contribute effectively to your team.</p>
        <p>My background includes ${experience}. I hold qualifications in ${education}, which complement my skills well. You can find more about me at <a href="${linkedin}" target="_blank">LinkedIn</a>.</p>
        <p>Thank you for considering my application. I look forward to the opportunity to discuss my fit for this role.</p>
        <p>Sincerely,<br>${name}</p>
      `;

      let cv = `
        <h2>Curriculum Vitae</h2>
        <p><strong>Name:</strong> ${name}</p>
        <p><strong>Title:</strong> ${title}</p>
        <p><strong>Email:</strong> ${email}</p>
        <p><strong>LinkedIn:</strong> <a href="${linkedin}" target="_blank">${linkedin}</a></p>
        <p><strong>Skills:</strong> ${skills}</p>
        <p><strong>Experience:</strong> ${experience}</p>
        <p><strong>Education:</strong> ${education}</p>
      `;

      let portfolio = template === 'modern' ? `
        <section style="font-family: sans-serif; padding: 40px; max-width: 600px; margin: auto;">
          <h1 style="font-size: 2em; color: #2d3748;">${name}</h1>
          <p><strong>Title:</strong> ${title}</p>
          <p><strong>Skills:</strong> ${skills}</p>
          <p><strong>What I Do:</strong> ${services}</p>
          <p><strong>Email:</strong> <a href="mailto:${email}">${email}</a></p>
          <p><strong>LinkedIn:</strong> <a href="${linkedin}" target="_blank">${linkedin}</a></p>
        </section>
      ` : `
        <div style="padding: 20px; font-family: Arial;">
          <h1>${name}</h1>
          <p><strong>Title:</strong> ${title}</p>
          <hr>
          <p><strong>Skills:</strong> ${skills}</p>
          <p><strong>Services:</strong> ${services}</p>
          <p><strong>Email:</strong> <a href="mailto:${email}">${email}</a></p>
          <p><strong>LinkedIn:</strong> <a href="${linkedin}" target="_blank">${linkedin}</a></p>
        </div>
      `;

      portfolioHtml = `
        <div style="font-family: Arial; padding: 20px;">
          ${portfolio}
          <hr style="margin: 30px 0;">
          ${cv}
          <hr style="margin: 30px 0;">
          ${coverLetter}
        </div>
      `;

      document.getElementById('result').innerHTML = portfolioHtml;
    }

    function downloadPortfolio() {
      const blob = new Blob([
        `<!DOCTYPE html><html><head><meta charset='UTF-8'><title>My Portfolio</title></head><body>${portfolioHtml}</body></html>`
      ], { type: 'text/html' });

      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'portfolio.html';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
    }
  </script>
</body>
</html>
