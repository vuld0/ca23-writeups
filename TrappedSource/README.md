# TRAPPEDSOURCE (Very easy)

**Note for readers: I did not solve this challenge during the CTF as it was solved by my teammate.**

- The Docker container was spawned, and we were presented with a digital lock for a door that needed to be opened.
- The code for the challenge was not provided, so we searched through the client-side code present in the "sources" of the browser page and found the script.js file. I have also attached the file in the project. 
- Upon opening the file, we discovered that the CONFIG.correctPin variable held the correct PIN for the digital lock:

```js
const checkPin = () => {
	pin = currentPin.join('')

	if (CONFIG.correctPin == pin) {
		fetch('/flag', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				'pin': CONFIG.correctPin
			})
		})
		.then((data) => data.json())
		.then((res) => {
			$('.lockStatus').css('font-size', '8px')
			$('.lockStatus').text(res.message)
		})
		return
	}

	$('.lockStatus').text('INVALID!')
	setTimeout(() => {
		reset()
	}, 3000)

}
```

- After providing the correct PIN, we were able to obtain the flag.
- You can find the flag in the flag.txt file.