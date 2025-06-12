// api/upload.js
const fs = require('fs');
const path = require('path');
const formidable = require('formidable');
const crypto = require('crypto');

module.exports = async (req, res) => {
  if (req.method !== 'POST') {
    res.status(405).send('Method not allowed');
    return;
  }

  const form = new formidable.IncomingForm({ keepExtensions: true });
  form.parse(req, (err, fields, files) => {
    if (err || !files.file) {
      res.status(400).json({ error: 'File upload error' });
      return;
    }

    const uploadedFile = files.file[0];
    const id = crypto.randomBytes(4).toString('hex');
    const savePath = path.join(__dirname, '..', 'sites', id);
    const outputFile = path.join(savePath, 'index.html');

    fs.mkdirSync(savePath, { recursive: true });
    fs.copyFileSync(uploadedFile.filepath, outputFile);

    res.status(200).json({ id });
  });
};
