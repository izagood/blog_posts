
# @ResponseBody 리턴시 한글 꺠짐

@RequestMapping(method = {RequestMethod.POST}, value = "/경로")

아래와 같이 추가

@RequestMapping(method = {RequestMethod.POST}, produces="application/json;charset=UTF-8", value = "/경로")


### 참조

[컨트롤러에서 @ResponseBody 리턴시 한글 깨짐 현상 해결](https://lasdri.tistory.com/795)