# HttpMessageConverter
## httpMessageConverter - 객체를 JSON/XML 으로 변환하자!
Spring MVC는 @RequestBody/@ResponseBody 요청/응답 데이터 변환 처리 시에 HttpMessageConverter를 이용한다.
만약 String 타입으로 변환한다면, StringHttpMessageConverter 클래스를 사용한다. 

WebMvcConfigurationSupport가 등록해준다.

//먼저 라이브러리가 추가되어 있는지 확인한다. 추가되어 있느면 True
//JSON
jackson2Present = ClassUtils.isPresent("com.fasterxml.jackson.databind.ObjectMapper", classLoader) && ClassUtils.isPresent("com.fasterxml.jackson.core.JsonGenerator", classLoader);
//XML
jackson2XmlPresent = ClassUtils.isPresent("com.fasterxml.jackson.dataformat.xml.XmlMapper", classLoader);
    
if (jackson2Present || gsonPresent || jsonbPresent) {
			map.put("json", MediaType.APPLICATION_JSON);
		}
//Default
		protected final void addDefaultHandlerExceptionResolvers

//라이브러리가 존재하면, MediaType을 맵에 담아둔다.
protected Map<String, MediaType> getDefaultMediaTypes() {
		Map<String, MediaType> map = new HashMap<>(4);
		if (romePresent) {
			map.put("atom", MediaType.APPLICATION_ATOM_XML);
			map.put("rss", MediaType.APPLICATION_RSS_XML);
		}
		if (!shouldIgnoreXml && (jaxb2Present || jackson2XmlPresent)) {
			map.put("xml", MediaType.APPLICATION_XML);
		}
		if (jackson2Present || gsonPresent || jsonbPresent) {
			map.put("json", MediaType.APPLICATION_JSON);
		}
		if (jackson2SmilePresent) {
			map.put("smile", MediaType.valueOf("application/x-jackson-smile"));
		}
		if (jackson2CborPresent) {
			map.put("cbor", MediaType.APPLICATION_CBOR);
		}
		return map;
	}
	

protected final List<HttpMessageConverter<?>> getMessageConverters() 
protected final void addDefaultHttpMessageConverters
	


### JSON
SpringBoot에서 spring-boot-starter-web 라이브러리에 spring-boot-starter-json이 의존성으로 추가되어있다.
spring-boot-starter-json안에 com.fasterxml.jackson.core:jackson-databind가 있는데, 이것이 JSON으로 ...
따라서 기본적으로 json이 의존성으로 추가되어 있기 때문에 별로도 메시지 컨버터를 등록하지 않는다면, spring-boot-starter-json을 사용하게 된다.
? Request와 Response는 데이터를 담을 형태를 어떻게 정하는가? HTTP의 header 정보를 참고한다. - MockMvc로 테스트하면 명확하게 볼 수 있다.


### XML
build.gradle에 의존성 추가을 추가하면, 알아서 메시지 컨터버로 등록해준다.
- implementation 'com.fasterxml.jackson.dataformat:jackson-dataformat-xml'

if (!shouldIgnoreXml && (jaxb2Present || jackson2XmlPresent)) {
			map.put("xml", MediaType.APPLICATION_XML);
		}
    
라이브러리만 추가했을 뿐인데.. 맘대로 바뀌었다..
