# 웹 개발 페이지 처리(Paging) 방법

## 웹 개발 페이지 처리

### 1. 전체 게시물의 개수를 가져온다 (totalCount)
```swift
  select count(*) as totalCount from board
```

### 2. 한 페이지에 몇 개의 게시글을 보여줄지 정한다. 
- listCount 등 10개, 20개 씩 보여준다..

### 3. 이제 게시판이 몇 개의 페이지를 가지는지 구할 수 있다. (총 페이지수, totalCount)
- totalPage = totalCount / listCount



```swift
   
   int totalCount = // DB 접속 후 쿼리를 통해 얻은 값 
   int listCount = 10;
   int totalPage = totalCount / listCount ;
   
   if( totalCount % listCount > 0){ // 나눠 떨어지지 않는 경우에 추가로 페이지가 하나 더 있어야하므로 +1을 해준다.
      totalPage++;     
   }
   
   if(totalPage < page){ // page가 현재 보고있는 페이지라고 가정 할때, url에서 임의로 page수를 바꿀 수도 있다.
      page = totalPage ;   // 총 페이지 수 보다 높은 페이지를 접근 하지 못하게 예방 
   }
   
```

### 4. 하단에 페이지 번호들을 몇 개 보여줄지 정한다. (PageCount 10개 =>  1 ~ 10 페이지,  11 ~ 21 페이지 .. )

### 5. 시작페이지와 끝페이지를 계산한다.

```swift
   // 현재 페이지가 pageCount와 같을 때를 유의하여 page-1 을 하고
   // +1 은 첫 페이지가 0 이나 10 이 아닌 => 1이나 11로 하기 위함 
   int startPage = ( (page - 1) / pageCount ) * pageCount + 1 ; 
   
   
   // -1은 첫 페이지가 1이나 11 등과 같을때 => 1~10 , 11~20 으로 지정하기 위함 
   int endPage = startPage + pageCount -1 ;
```

### 6. 대신 5. 와 같이 끝페이지를 계산해 버리면 totalPage(총 페이지수)보다 크게 잡힐 위험이 있으니 그것을 처리해야 함 

```swift
   if(endPage > totalPage){
      endPage = totalPage;
   }
```

### 7. 처음 / 끝 / 이전 / 다음 
- 처음 : page = 1
- 끝 : page = totalPage
- 이전 : page -1
- 다음 : page +1


<br/>
<hr/>

<br/>

# 샘플 jsp

```swift
   <%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%@ taglib uri = "http://java.sun.com/jsp/jstl/core" prefix="c" %>    

 
<script type="text/javascript">

var pagePerRecord; // 페이지 전체 크기 

function search(i){
    
     if(i != undefined && i != ""){
    	 document.getElementById("pageIndex").value = i;
     }	  		   
		   document.getElementById("search").submit();
 }	

function pageChange(type){
	var lastPage = "${search.pageCount}";
	var pageIndex = document.getElementById("pageIndex");
	
	switch(type){
	   case 1 :
		   document.getElementById("pageIndex").value = 1;
		   break;
	   case 2 :
		   if(pageIndex.value > 1){
			   pageIndex.value = Number(pageIndex.value) -1;
		   }
		   break;
	   case 3 : 
		   if(pageIndex.value < lastPage){
			   pageIndex.value = Number(pageIndex.value) +1;
		   }
		   break;
	   case 4 :
		   document.getElementById("pageIndex").value = lastPage;
		   break;
	}
	document.getElementById("search").submit();
}

  window.onload = function(){
	  document.getElementById("pagePerRecord").value = "${search.pagePerRecord}";
  }

</script>



<p>list 내용 출력</p>
<form id = "search" method = "post" action="/userInfo/list.do">

   <input type = "hidden" id = "pageIndex" name = "pageIndex" value="${search.pageIndex}" />
   
   <select id = "pagePerRecord" name = "pagePerRecord" onchange = "javascript:search();">
      <option value = "2">2</option>
      <option value = "5">5</option>
      <option value = "10">10</option>
   </select> 
   <!-- <input type = "hidden" id = "pagePerRecord" name = "pagePerRecord"/>  -->
     
   <!-- pageIndex라는 이름으로 넘기면 자동으로 Search 클래스에서 setter 메서드로 매핑 시켜줌 -->
</form>

<table border = "1">
  <tr>
      <th>아이디</th>
      <th>사용자명</th>
      <th>이메일</th>
      <th>날짜</th>
      <th>고객</th>
  </tr>
  <c:forEach var = "obj" items="${list}">
     <tr>
        <td><a href="/userInfo/view.do?userId=${obj.userId}"><c:out value="${obj.userId}"/></a></td>
        <td><c:out value="${obj.userName}"/></td>
        <td><c:out value="${obj.email}"/></td>
        <td><c:out value="${obj.date}"/></td>
        <td><a href="/quality/insert_form.do?userId=${obj.userId}"><c:out value="선택"/></a></td>
     </tr>
  </c:forEach>
</table>

<br/>
<br/>

<!-- 페이지 넘버링 버튼 -->
<div>

     <button onclick="javascript:pageChange(1)">처음</button>
     <button onclick="javascript:pageChange(2)">이전</button>
    
<c:forEach begin = "1" end="${search.pageCount}" varStatus="i">
    <button 
        <c:if test="${search.pageIndex eq i.index}">style="background-color:#000;color:#fff"</c:if>
        onclick="javascript:search('${i.index}');"
    >${i.index}</button>
</c:forEach>
      <button onclick="javascript:pageChange(3)">다음</button>
      <button onclick="javascript:pageChange(4)">끝</button>  
</div>

<div>
   페이지 입력 : <input type = "number" placeholder="원하는 페이지 입력..." onchange="javascript:search(this.value)"/>(숫자만 가능)
</div>

 <div>
   현재 페이지 : ${search.pageIndex} / 전체 페이지 : ${search.pageCount} / 전체 갯수 : ${search.recordCount}  
 </div>

```


<hr/>

<br/>

# 샘플 2

### Paging Vo : setTotalCount (int totalCount) 호출시 => makePaging() 함수 호출 함 
    
```swift
    
   public class Paging {
    private int pageSize; // 게시 글 수
    private int firstPageNo; // 첫 번째 페이지 번호
    private int prevPageNo; // 이전 페이지 번호
    private int startPageNo; // 시작 페이지 (페이징 네비 기준)
    private int pageNo; // 페이지 번호
    private int endPageNo; // 끝 페이지 (페이징 네비 기준)
    private int nextPageNo; // 다음 페이지 번호
    private int finalPageNo; // 마지막 페이지 번호
    private int totalCount; // 게시 글 전체 수

    /**
     * @return the pageSize
     */
    public int getPageSize() {
        return pageSize;
    }

    /**
     * @param pageSize the pageSize to set
     */
    public void setPageSize(int pageSize) {
        this.pageSize = pageSize;
    }

    /**
     * @return the firstPageNo
     */
    public int getFirstPageNo() {
        return firstPageNo;
    }

    /**
     * @param firstPageNo the firstPageNo to set
     */
    public void setFirstPageNo(int firstPageNo) {
        this.firstPageNo = firstPageNo;
    }

    /**
     * @return the prevPageNo
     */
    public int getPrevPageNo() {
        return prevPageNo;
    }

    /**
     * @param prevPageNo the prevPageNo to set
     */
    public void setPrevPageNo(int prevPageNo) {
        this.prevPageNo = prevPageNo;
    }

    /**
     * @return the startPageNo
     */
    public int getStartPageNo() {
        return startPageNo;
    }

    /**
     * @param startPageNo the startPageNo to set
     */
    public void setStartPageNo(int startPageNo) {
        this.startPageNo = startPageNo;
    }

    /**
     * @return the pageNo
     */
    public int getPageNo() {
        return pageNo;
    }

    /**
     * @param pageNo the pageNo to set
     */
    public void setPageNo(int pageNo) {
        this.pageNo = pageNo;
    }

    /**
     * @return the endPageNo
     */
    public int getEndPageNo() {
        return endPageNo;
    }

    /**
     * @param endPageNo the endPageNo to set
     */
    public void setEndPageNo(int endPageNo) {
        this.endPageNo = endPageNo;
    }

    /**
     * @return the nextPageNo
     */
    public int getNextPageNo() {
        return nextPageNo;
    }

    /**
     * @param nextPageNo the nextPageNo to set
     */
    public void setNextPageNo(int nextPageNo) {
        this.nextPageNo = nextPageNo;
    }

    /**
     * @return the finalPageNo
     */
    public int getFinalPageNo() {
        return finalPageNo;
    }

    /**
     * @param finalPageNo the finalPageNo to set
     */
    public void setFinalPageNo(int finalPageNo) {
        this.finalPageNo = finalPageNo;
    }

    /**
     * @return the totalCount
     */
    public int getTotalCount() {
        return totalCount;
    }

    /**
     * @param totalCount the totalCount to set
     */
    public void setTotalCount(int totalCount) {
        this.totalCount = totalCount;
        this.makePaging();
    }

    /**
     * 페이징 생성
     */
    private void makePaging() {
        if (this.totalCount == 0) return; // 게시 글 전체 수가 없는 경우
        if (this.pageNo == 0) this.setPageNo(1); // 기본 값 설정
        if (this.pageSize == 0) this.setPageSize(10); // 기본 값 설정

        int finalPage = (totalCount + (pageSize - 1)) / pageSize; // 마지막 페이지
        if (this.pageNo > finalPage) this.setPageNo(finalPage); // 기본 값 설정

        if (this.pageNo < 0 || this.pageNo > finalPage) this.pageNo = 1; // 현재 페이지 유효성 체크

        boolean isNowFirst = pageNo == 1 ? true : false; // 시작 페이지 (전체)
        boolean isNowFinal = pageNo == finalPage ? true : false; // 마지막 페이지 (전체)

        int startPage = ((pageNo - 1) / 10) * 10 + 1; // 시작 페이지 (페이징 네비 기준)
        int endPage = startPage + 10 - 1; // 끝 페이지 (페이징 네비 기준)

        if (endPage > finalPage) { // [마지막 페이지 (페이징 네비 기준) > 마지막 페이지] 보다 큰 경우
            endPage = finalPage;
        }

        this.setFirstPageNo(1); // 첫 번째 페이지 번호

        if (isNowFirst) {
            this.setPrevPageNo(1); // 이전 페이지 번호
        } else {
            this.setPrevPageNo(((pageNo - 1) < 1 ? 1 : (pageNo - 1))); // 이전 페이지 번호
        }

        this.setStartPageNo(startPage); // 시작 페이지 (페이징 네비 기준)
        this.setEndPageNo(endPage); // 끝 페이지 (페이징 네비 기준)

        if (isNowFinal) {
            this.setNextPageNo(finalPage); // 다음 페이지 번호
        } else {
            this.setNextPageNo(((pageNo + 1) > finalPage ? finalPage : (pageNo + 1))); // 다음 페이지 번호
        }

        this.setFinalPageNo(finalPage); // 마지막 페이지 번호
    }

    @Override
    public String toString() {
        return ToStringBuilder.reflectionToString(this, ToStringStyle.SHORT_PREFIX_STYLE);
    }
}


```

### 2. Controller : setTotalCount(totalCount)를 호출한다. 

```swift
  @RequestMapping(value="/list", method=RequestMethod.GET)
public ModelAndView list(Sample sample) throws Exception {
    try {
        // (Before) Doing...

        Paging paging = new Paging();
        paging.setPageNo(1);
        paging.setPageSize(10);
        paging.setTotalCount(totalCount);


        // (After) Doing...
    } catch (Exception e) {
        throw e;
    }
}

```

### 3. paging.jsp  :  View 스타일에 따라 수정이 가능

```swift
    <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<div class="paginate">
    <a href="javascript:goPage(${param.firstPageNo})" class="first">처음 페이지</a>
    <a href="javascript:goPage(${param.prevPageNo})" class="prev">이전 페이지</a>
    <span>
        <c:forEach var="i" begin="${param.startPageNo}" end="${param.endPageNo}" step="1">
            <c:choose>
                <c:when test="${i eq param.pageNo}"><a href="javascript:goPage(${i})" class="choice">${i}</a></c:when>
                <c:otherwise><a href="javascript:goPage(${i})">${i}</a></c:otherwise>
            </c:choose>
        </c:forEach>
    </span>
    <a href="javascript:goPage(${param.nextPageNo})" class="next">다음 페이지</a>
    <a href="javascript:goPage(${param.finalPageNo})" class="last">마지막 페이지</a>
</div>


```

### 4. list.jsp : paging.jsp를 호출

```swift
  // (Before) Doing...
<jsp:include page="paging.jsp" flush="true">
    <jsp:param name="firstPageNo" value="${paging.firstPageNo}" />
    <jsp:param name="prevPageNo" value="${paging.prevPageNo}" />
    <jsp:param name="startPageNo" value="${paging.startPageNo}" />
    <jsp:param name="pageNo" value="${paging.pageNo}" />
    <jsp:param name="endPageNo" value="${paging.endPageNo}" />
    <jsp:param name="nextPageNo" value="${paging.nextPageNo}" />
    <jsp:param name="finalPageNo" value="${paging.finalPageNo}" />
</jsp:include>
// (After) Doing...

```
