---
showforum: true
projectname: Minke Open Calls Projects
demo_project_url: https://oscgonfer.github.io/sc-book
projects:
  - [Demo, https://fablabbcn.github.io/smartcitizen-minke-template]
  - [ACTIVATE, https://oscgonfer.github.io/sc-book]
  - [SmartCoKLIMINKE, https://oscgonfer.github.io/sc-book]  
---

# Projects

This section will host the results and discussions around the different projects during the MINKE project [Open Calls](https://minke.eu/services/apply-for-tna-va/) with Low Cost sensors.

!!! info "Let's do this!"
	If you are part of a project in the Open calls, you will have free access to sensors and the team's support for your projects. The only thing we ask in return is to make sure to **document the project with care**. For this, we think that sharing the results of the project, as well as your data and findings is very important. We have prepared a good guide available in our [demo project book project]({{ demo_project_url }}). With this we hope to encourage sharing knowledge with other projects. Finally, remember that you can use **our forum** to interact with your own local community if you wish!

<div style="display: grid; grid-gap: 30px 10px; grid-template-columns: 1fr 1fr; grid-template-rows:  1fr 1fr;">
	{%- for x in projects %}
		<a href={{ x[1] }}>
			<div style="display: block;text-align:center">
				<img src="{{ x[1] + '/_static/logo.png' }}" width=400px>
				<span style="font-style: italic;font-weight: lighter;">{{ x[0] }}</span>
			</div>
		</a>
	{%- endfor %}
</div>
